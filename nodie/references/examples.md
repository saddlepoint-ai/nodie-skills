# Nodie DSL Examples

## RSS to Slack (YAML)

```yaml
name: HN Top Stories to Slack
nodes:
  - id: trigger_1
    type: trigger.manual
    name: Start
    params: {}
    next: [fetch_rss_1]

  - id: fetch_rss_1
    type: rss.read
    name: Fetch HN Feed
    params:
      url: "https://hnrss.org/frontpage?count=5"
    next: [format_articles_1]

  - id: format_articles_1
    type: code
    name: Format Articles
    params:
      articles: $fetch_rss_1
      code: |
        items = input['articles']
        text = "\n".join(f"- {a['title']}: {a['link']}" for a in items)
        result = {'text': text}
    next: [summarize_1]

  - id: summarize_1
    type: openai_chat
    name: Summarize Articles
    params:
      api_key: $env['OPENAI_API_KEY']
      model: "gpt-4o-mini"
      prompt: "Summarize these HN top stories into a brief digest:\n${{ format_articles_1['text'] }}"
    next: [send_slack_1, output_1]

  - id: send_slack_1
    type: slack.post_message
    name: Post to Slack
    params:
      credential: slack
      channel: "#tech-news"
      text: $summarize_1['content']
    next: []

  - id: output_1
    type: output
    name: Output
    params:
      outputs:
        - type: text
          value: $summarize_1['content']
          label: "Summary"
        - type: text
          value: $format_articles_1['text']
          label: "Article Links"
    next: []
```

## Supabase Query (JSON)

When generating JSON DSL, use this exact structure:

```json
{
  "name": "Query Today Workspaces",
  "nodes": [
    {
      "id": "trigger_1",
      "type": "trigger.manual",
      "name": "Start",
      "params": {},
      "next": ["query_db_1"]
    },
    {
      "id": "query_db_1",
      "type": "supabase.execute",
      "name": "Query Workspaces",
      "params": {
        "credential": "supabase",
        "operation": "select",
        "table": "workspace",
        "filters": {
          "created_at": {"gte": "2024-01-01"}
        },
        "columns": ["id", "name", "created_at"],
        "limit": 100
      },
      "next": ["format_result_1"]
    },
    {
      "id": "format_result_1",
      "type": "code",
      "name": "Format Result",
      "params": {
        "raw": "$query_db_1",
        "code": "data = input['raw']\nresult = {'count': len(data.get('data', [])), 'rows': data.get('data', [])}"
      },
      "next": ["output_1"]
    },
    {
      "id": "output_1",
      "type": "output",
      "name": "Output",
      "params": {
        "outputs": [
          {
            "type": "json",
            "value": "$format_result_1",
            "label": "Query Result"
          }
        ]
      },
      "next": []
    }
  ]
}
```

## AI Image Generation + Save to Notion (JSON)

```json
{
  "name": "Avatar Generator & Notion Saver",
  "nodes": [
    {
      "id": "trigger_1",
      "type": "trigger.manual",
      "name": "Start",
      "params": {},
      "next": ["generate_avatars_1"]
    },
    {
      "id": "generate_avatars_1",
      "type": "openai.image",
      "name": "Generate Avatars",
      "params": {
        "api_key": "$env['OPENAI_API_KEY']",
        "prompt": ["A friendly blue robot avatar", "A wise purple mage avatar"],
        "size": "1024x1024",
        "model": "dall-e-3"
      },
      "next": ["save_to_notion_1"]
    },
    {
      "id": "save_to_notion_1",
      "type": "notion.append_blocks",
      "name": "Save to Notion",
      "params": {
        "credential": "notion",
        "block_id": "123456",
        "blocks": [
          {
            "object": "block",
            "type": "image",
            "image": {
              "type": "external",
              "external": { "url": "$generate_avatars_1['results'][0]" }
            }
          },
          {
            "object": "block",
            "type": "image",
            "image": {
              "type": "external",
              "external": { "url": "$generate_avatars_1['results'][1]" }
            }
          }
        ]
      },
      "next": ["output_1"]
    },
    {
      "id": "output_1",
      "type": "output",
      "name": "Display Results",
      "params": {
        "outputs": [
          {
            "type": "image",
            "value": "$generate_avatars_1['results']",
            "label": "Generated Avatars"
          },
          {
            "type": "text",
            "value": "Successfully saved to Notion page 3030aabdb48180288709d97b37131bbe",
            "label": "Status"
          }
        ]
      },
      "next": []
    }
  ]
}
```

## XHS Search + Get Comments (JSON)

```json
{
  "name": "XHS Brand Monitoring with Comments",
  "nodes": [
    {
      "id": "trigger_manual_1",
      "type": "trigger.manual",
      "name": "Start",
      "params": {},
      "next": ["search_xhs_1"]
    },
    {
      "id": "search_xhs_1",
      "type": "xhs.search",
      "name": "Search XHS",
      "params": {
        "keywords": "brand_name",
        "max_items": 10,
        "sort_by": "time_descending",
        "note_type": "all"
      },
      "next": ["extract_urls_1"]
    },
    {
      "id": "extract_urls_1",
      "type": "code",
      "name": "Extract Post URLs",
      "params": {
        "search_results": "$search_xhs_1",
        "code": |
          results = input['search_results']
          urls = []
          if results and 'notes' in results:
            for note in results['notes']:
              if 'link' in note:
                urls.append(note['link'])
          result = {'post_urls': urls[:5]}
      },
      "next": ["get_comments_1"]
    },
    {
      "id": "get_comments_1",
      "type": "xhs.get_comments",
      "name": "Get Comments",
      "params": {
        "post_urls": "$extract_urls_1['post_urls']",
        "max_pages": 3,
        "sort_strategy": "like_count"
      },
      "next": ["output_1"]
    },
    {
      "id": "output_1",
      "type": "output",
      "name": "Display Results",
      "params": {
        "outputs": [
          {
            "type": "json",
            "value": "$search_xhs_1",
            "label": "Search Results"
          },
          {
            "type": "json",
            "value": "$get_comments_1",
            "label": "Comments"
          }
        ]
      },
      "next": []
    }
  ]
}
```

## Reddit Search with Markdown Table (JSON) - Correct Pattern

This example demonstrates the **correct** way to generate Markdown tables for output nodes. All formatting logic must be done in a `code` node, then referenced in the `output` node.

```json
{
  "name": "Scrape Reddit Posts about OpenClaw",
  "nodes": [
    {
      "id": "trigger_1",
      "type": "trigger.manual",
      "name": "Start",
      "params": {},
      "next": ["search_reddit_1"]
    },
    {
      "id": "search_reddit_1",
      "type": "reddit.search",
      "name": "Search Reddit for OpenClaw",
      "params": {
        "sort": "relevance",
        "query": "openclaw",
        "max_items": 10,
        "credential": "apify_system",
        "search_type": "search",
        "time_filter": "all",
        "include_comments": false
      },
      "next": ["format_results_1"]
    },
    {
      "id": "format_results_1",
      "type": "code",
      "name": "Format Results",
      "params": {
        "posts": "$search_reddit_1['posts']",
        "total": "$search_reddit_1['total']",
        "code": "posts = input.get('posts', [])\ntotal = input.get('total', 0)\n\nformatted_posts = []\ntable_rows = []\n\nfor i, post in enumerate(posts, 1):\n    rank = i\n    title = post.get('title', 'N/A')\n    author = post.get('author', 'N/A')\n    subreddit = post.get('subreddit', 'N/A')\n    upvotes = post.get('upvotes', 0)\n    comments = post.get('comments', 0)\n    url = post.get('url', 'N/A')\n    \n    # Process title truncation in Python\n    short_title = (title[:30] + '...') if len(title) > 30 else title\n    \n    # Generate Markdown table row\n    row = f\"| {rank} | {short_title} | {author} | {subreddit} | {upvotes} | {comments} | [Link]({url}) |\"\n    table_rows.append(row)\n    \n    formatted_posts.append({\n        'rank': rank,\n        'title': title,\n        'author': author,\n        'subreddit': subreddit,\n        'upvotes': upvotes,\n        'comments': comments,\n        'url': url\n    })\n\n# Join table rows into a single string\nresult = {\n    'posts': formatted_posts, \n    'total': total, \n    'table_text': '\\n'.join(table_rows)\n}"
      },
      "next": ["output_1"]
    },
    {
      "id": "output_1",
      "type": "output",
      "name": "Complete",
      "params": {
        "outputs": [
          {
            "type": "markdown",
            "label": "Reddit Posts",
            "value": "📊 **Reddit OpenClaw Search Results**\n\nTotal posts found: ${{format_results_1['total']}}\n\n| # | Title | Author | Subreddit | Upvotes | Comments | URL |\n|---|-------|--------|-----------|---------|----------|-----|\n${{format_results_1['table_text']}}"
          }
        ]
      },
      "next": []
    }
  ]
}
```

**Key points:**
- ✅ All formatting logic (loops, string manipulation, table generation) is done in the `code` node
- ✅ The `code` node outputs a ready-to-use `table_text` string field
- ✅ The `output` node simply references `${{ format_results_1['table_text'] }}` - no logic in `${{ }}`
- ❌ **WRONG**: Do NOT try to use `.map()`, `.join()`, or other expressions inside `${{ }}` in the output node
