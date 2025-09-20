# Radish Immersive Website

A modern, responsive website for Radish Immersive Creative Studio featuring immersive storytelling, interactive design, and thought leadership content.

## Features

- **Responsive Design**: Mobile-first approach with smooth animations
- **Interactive Elements**: Hover effects, smooth scrolling, and dynamic content
- **Thought Leadership**: Insights section with filtering capabilities
- **Case Studies**: Detailed project showcases
- **Contact Integration**: Working contact form with email integration
- **Modern UI**: Clean design with radish-inspired color scheme

## Pages

- **Home**: Hero section with company overview
- **About**: Team information and company statistics
- **Insights**: Thought leadership content with category filtering
- **Work**: Portfolio showcase with case study links
- **Contact**: Contact form and company information

## Technology Stack

- **HTML5**: Semantic markup
- **CSS3**: Modern styling with CSS Grid and Flexbox
- **JavaScript**: Vanilla JS for interactivity
- **Fonts**: Inter from Google Fonts
- **Icons**: Custom radish favicon

## Deployment

This site is configured for deployment on AWS Amplify with automatic CI/CD.

### Prerequisites
- GitHub repository
- AWS account
- Domain configured in Route 53

### Quick Deploy
1. Push code to GitHub
2. Connect to AWS Amplify
3. Configure custom domain
4. Deploy automatically

See `amplify-deployment-guide.md` for detailed instructions.

## Local Development

```bash
# Serve locally
python -m http.server 8000
# or
npx serve .

# Open in browser
open http://localhost:8000
```

## File Structure

```
├── index.html                          # Homepage
├── insights.html                       # Insights page
├── future-immersive-storytelling.html  # Article page
├── case-study.html                     # Case study page
├── styles.css                          # Main stylesheet
├── script.js                           # JavaScript functionality
├── floating-radish.png                 # Hero image
├── floating-radish-favicon.png         # Favicon
├── amplify.yml                         # Amplify configuration
├── package.json                        # Node.js dependencies
└── README.md                           # This file
```

## Color Scheme

- **Primary Red**: #fb4e40
- **Primary Green**: #397e58
- **Black**: #2c3e50
- **White**: #ffffff
- **Light Gray**: #f8f9fa

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers

## License

© 2025 Radish Immersive. All rights reserved.
