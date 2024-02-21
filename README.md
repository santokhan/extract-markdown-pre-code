# extract-markdown-pre-code

A beautifully simple concept for extracting `<pre><code>` blocks from rendered AI-generated Markdown.

This is useful for implementing custom applications utilizing the **ChatGPT API**.

## Split code
```javascript
const markdown_string = `
<p>Others</p>
<pre>
  <code>Code block</code>
</pre>
<a href=""><strong>Others</strong></a>
`; /** your html code here */
const split_html_by_pre_tag = markdown_string
  .replaceAll("<pre>", "---")
  .replaceAll("</pre>", "---")
  .split("---");
```

## Categorize

```javascript
split_html_by_pre_tag
  .map((html, idx) => ({
    [idx % 2 ? "code" : "others"]: html.trim(),
  }))
  .filter(({ code, others }) => code || others);
```

## Output

```javascript
[
  {
    others: '<p>Others</p>'
  },
  {
    code: '<code>Code block</code>'
  },
  {
    others: '<a href=""><strong>Anchor</strong></a>'
  }
]
```
