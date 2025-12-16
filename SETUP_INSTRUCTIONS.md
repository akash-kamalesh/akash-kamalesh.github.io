# Portfolio Setup Instructions

Your Zola portfolio has been created! Here's what you need to customize:

## 1. Update Personal Information

Edit `config.toml` and update these values:

```toml
[extra]
name = "Your Name"                                    # Your full name
email = "your.email@example.com"                      # Your email address
github = "https://github.com/akash-kamalesh"           # Your GitHub profile URL
linkedin = "https://linkedin.com/in/yourprofile"      # Your LinkedIn profile URL
resume_url = "https://drive.google.com/file/d/YOUR_RESUME_ID/view"  # Your resume link
```

## 2. Add Your Profile Picture

1. Place your profile picture in the `static/` folder
2. Name it `profile.jpg` (or update the filename in `templates/index.html` if you use a different name)
3. The image will be displayed as a circular profile picture in the hero section

## 3. Add Blog Posts

To add blog posts:

1. Create a new markdown file in `content/blog/` folder
2. Example: `content/blog/my-first-post.md`
3. Use this format:

```markdown
+++
title = "My First Blog Post"
date = 2024-01-15
description = "A brief description of your post"
+++

Your blog content goes here...
```

## 4. Build and Run Locally

To preview your site locally:

```bash
zola serve
```

Your site will be available at `http://localhost:1111`

## 5. Deploy to GitHub Pages

After building with `zola build`, deploy the `public/` folder to your GitHub Pages repository.

## File Structure

```
personalpage/
├── config.toml              # Site configuration
├── content/
│   └── blog/
│       └── _index.md        # Blog section
├── static/
│   ├── style.css            # Main stylesheet
│   └── profile.jpg          # Your profile picture
├── templates/
│   ├── base.html            # Base template with navbar
│   ├── index.html           # Home page template
│   └── blog.html            # Blog listing template
└── index.markdown           # Home page content
```

## Features Included

✅ Sticky navigation bar with:
- About link (scrolls to about section)
- Resume link (opens Google Drive)
- Blog link (goes to blog page)
- GitHub icon (redirects to GitHub)
- LinkedIn icon (redirects to LinkedIn)
- Email icon (opens email client)

✅ Hero section with:
- Circular profile picture
- Your name
- Professional subtitle

✅ About section with your research and experience

✅ Blog section (ready for your posts)

✅ Responsive design (works on mobile, tablet, desktop)

✅ Modern styling with smooth animations

## Customization Tips

- **Colors**: Edit the CSS variables in `static/style.css` (`:root` section)
- **Fonts**: Change the font-family in `static/style.css`
- **Layout**: Modify templates in `templates/` folder
- **Content**: Edit markdown files in `content/` folder

Happy blogging! 🚀
