# Alina Ahsan - Professional Portfolio

A modern, responsive portfolio website built with Vue.js showcasing Alina Ahsan's professional experience, education, and skills.

## 🌟 Features

- **Modern Design**: Clean, professional layout with gradient backgrounds and smooth animations
- **Responsive**: Fully responsive design that looks great on all devices
- **Interactive**: Smooth scrolling navigation with active link highlighting
- **Professional**: Comprehensive sections covering all CV information
- **Fast**: Built with Vite for optimal performance

## 🚀 Getting Started

### Prerequisites

- Node.js (version 16 or higher)
- npm or yarn

### Installation

1. Clone this repository:
```bash
git clone <your-repo-url>
cd Portfolio
```

2. Install dependencies:
```bash
npm install
```

3. **IMPORTANT**: Add your photo
   - Save your graduation photo as `alina.png` in the `src/assets/` folder
   - Use the professional photo showing you with your gold medal
   - Recommended size: 400x400px or similar square format
   - File format: PNG (to preserve quality of your graduation photo)

4. Start the development server:
```bash
npm run dev
```

5. Open your browser and visit `http://localhost:5173`

## 📸 Photo Setup

**Important**: You need to add your graduation photo to the portfolio.

1. Save your photo (the one showing you with the gold medal in graduation attire) as `alina.png`
2. Place it in the `src/assets/` folder
3. The photo will automatically appear in your portfolio

## 🚀 Deployment to Netlify

### Method 1: Drag & Drop (Easiest)

1. Build the project:
```bash
npm run build
```

2. Go to [Netlify](https://www.netlify.com/)
3. Drag and drop the `dist` folder to Netlify's deployment area
4. Your site will be live immediately!

### Method 2: Git Integration (Recommended for updates)

1. Push your code to GitHub/GitLab
2. Connect your repository to Netlify
3. Set build settings:
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`
4. Deploy!

### Custom Domain (Optional)

1. In Netlify dashboard, go to Site settings > Domain management
2. Add your custom domain
3. Follow the DNS configuration instructions

## 🛠️ Customization

### Updating Content

- All content is in `src/App.vue`
- Modify text, add new sections, or update information as needed
- Colors and styling can be adjusted in `src/style.css`

### Color Scheme

The portfolio uses a professional color palette defined in CSS variables:
- Primary: `#6366f1` (Indigo)
- Secondary: `#8b5cf6` (Purple)
- Accent: `#f59e0b` (Amber)

To change colors, update the CSS variables in `src/style.css`.

## 📱 Responsive Design

The portfolio is fully responsive and optimized for:
- Desktop (1200px+)
- Tablet (768px - 1199px)
- Mobile (320px - 767px)

## 🎨 Design Features

- **Gradient Header**: Eye-catching gradient background with subtle pattern
- **Smooth Animations**: Scroll-triggered animations and hover effects
- **Professional Typography**: Clean fonts (Inter & Poppins) for optimal readability
- **Card-based Layout**: Organized content in easy-to-read cards
- **Sticky Navigation**: Navigation bar stays visible while scrolling

## 📧 Contact Information

The portfolio includes your contact details:
- **Email**: alina.ahsan13@gmail.com
- **Phone**: +91-6386821493
- **Address**: Lucknow, India

## 🔧 Technical Stack

- **Framework**: Vue.js 3
- **Build Tool**: Vite
- **Styling**: Modern CSS with custom properties
- **Deployment**: Netlify-ready

## 📄 License

This project is for personal use by Alina Ahsan.

---

**Built with ❤️ for showcasing professional excellence**
