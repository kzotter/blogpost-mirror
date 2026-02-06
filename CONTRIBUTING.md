# Adding New Posts

This document describes the format for adding new posts to this repository.

## Post Structure

Each post lives in its own folder under `posts/`:

```
posts/
└── YYYY-MM-DD-slug/
    ├── post.md         # The article content
    ├── qa.md           # Q&A companion for AI
    └── metadata.json   # Structured metadata
```

## post.md Format

```markdown
# Post Title

Your post content here...
```

## qa.md Format

```markdown
# Q&A: Post Title

**Q: What is the main thesis of this post?**

A: [Answer]

**Q: Who is the target audience?**

A: [Answer]

**Q: What are the key takeaways?**

A: [Answer]

**Q: How does this relate to dedicated device management?**

A: [Answer]

[Add more Q&A pairs as relevant to the content]
```

## metadata.json Format

```json
{
  "title": "Post Title",
  "date": "2026-02-06",
  "author": "Keith Szot",
  "source": "substack",
  "source_url": "https://substack.com/@kzotter/p/post-slug",
  "canonical_url": "https://substack.com/@kzotter/p/post-slug",
  "tags": ["Edge AI", "Dedicated Devices", "IT Operations"],
  "description": "A brief 1-2 sentence summary.",
  "topics": ["edge-ai", "dedicated-device-management"]
}
```

## After Adding a Post

Update these index files:
- `docs/index.md` - Add to appropriate sections
- `llms.txt` - Add to Posts section  
- `llms-full.txt` - Append full post + Q&A content
- `sitemap.xml` - Add URL entry
