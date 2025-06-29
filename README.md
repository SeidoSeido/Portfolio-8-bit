# 8-Bit Themed Portfolio Website

A retro-inspired, interactive portfolio website built with Vue.js featuring an authentic 8-bit aesthetic and modern functionality. This portfolio showcases frontend development skills through nostalgic design elements and smooth scroll-triggered animations.

## Features

- **8-Bit Hero Section**: Features an interactive Pong mini-game with retro styling and keyboard controls
- **Animated About Section**: CRT screen effects with scanlines, pixel grid, chromatic aberration, and animated code terminal
- **Scroll-Triggered Animations**: Creative pixel-themed animations for all sections using IntersectionObserver
- **Retro Typography**: "Press Start 2P" pixel font throughout the site for authentic 8-bit feel
- **Interactive Skills Section**: Animated progress bars with pixelated styling and glitch effects
- **Filterable Project Gallery**: Dynamic project filtering with smooth animations and hover effects
- **Responsive Design**: Fully responsive across all devices while maintaining retro aesthetic
- **Modern Performance**: Built with Vite for fast development and optimized production builds

## Technologies Used

- **Vue.js 3** - Progressive JavaScript framework with Composition API
- **Vite** - Next-generation frontend build tool
- **CSS3** - Advanced styling with keyframe animations, CSS Grid, and Flexbox
- **HTML5** - Semantic markup structure
- **JavaScript ES6+** - Modern JavaScript with IntersectionObserver API
- **Google Fonts** - "Press Start 2P" font for authentic 8-bit typography
- **CSS Animations** - Custom keyframe animations for retro effects

## Getting Started

### Prerequisites

- Node.js (version 14 or higher)
- npm or yarn

### Installation

1. Clone the repository or download the files
2. Navigate to the project directory:
   ```bash
   cd Portfolio-8-bit
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

5. Open your browser and visit `http://localhost:5173`

### Building for Production

To build the project for production:

```bash
npm run build
```

The built files will be in the `dist` directory.

## Project Structure

```
src/
├── components/
│   ├── Navigation.vue      # 8-bit styled navigation with mobile menu
│   ├── HeroSection.vue     # Landing section with Pong mini-game
│   ├── AboutSection.vue    # CRT screen effects with animated terminal
│   ├── SkillsSection.vue   # Pixelated skills with progress animations
│   ├── ProjectsSection.vue # Filterable project gallery with retro styling
│   └── ContactSection.vue  # Contact form with pixel animations
├── App.vue                 # Main application component
├── main.js                 # Application entry point
└── style.css              # Global 8-bit styles and animations
```

## Key Features Breakdown

### 8-Bit Visual Effects
- **CRT Screen Simulation**: Scanlines, pixel grid, and chromatic aberration effects
- **Glitch Animations**: Subtle character glitching in section titles
- **Pixel Perfect Typography**: Consistent use of retro gaming fonts
- **Color Palette**: Authentic 8-bit color scheme with neon accents

### Interactive Elements
- **Pong Mini-Game**: Fully functional Pong game in the hero section
- **Scroll Animations**: Custom pixel-themed animations triggered by viewport intersection
- **Hover Effects**: Retro-styled hover states for all interactive elements
- **Animated Terminal**: Live-typing code animation with syntax highlighting

### Performance Optimizations
- **Lazy Loading**: Animations only trigger when elements enter viewport
- **Efficient Rendering**: Optimized CSS animations and transitions
- **Responsive Design**: Maintains performance across all device sizes
- **Modern Build Process**: Vite ensures fast development and optimized production builds

## Customization

### Personal Information

Update the following components with your personal information:

1. **HeroSection.vue**: Modify the developer name and Pong game settings
2. **AboutSection.vue**: Update about text, statistics, and code terminal content
3. **SkillsSection.vue**: Customize skills, progress levels, and categories
4. **ProjectsSection.vue**: Replace with your actual projects and filter categories
5. **ContactSection.vue**: Update contact information and social links

### Styling and Themes

- **Global Styles**: Main 8-bit theme defined in `src/style.css`
- **Component Styles**: Each Vue component contains scoped styling
- **Color Customization**: Modify CSS custom properties for color scheme changes
- **Animation Timing**: Adjust animation delays and durations in component styles
- **Font Loading**: "Press Start 2P" font loaded via Google Fonts

### Mini-Game Customization

The Pong mini-game in the hero section includes:
- **Paddle Controls**: Arrow key navigation with smooth movement
- **Ball Physics**: Realistic bounce mechanics and speed variations
- **Visual Styling**: Retro pixel-perfect graphics
- **Responsive Design**: Adapts to different screen sizes
- **Performance**: Optimized game loop with requestAnimationFrame

## Browser Support

This portfolio is optimized for modern browsers with full CSS animation support:

- **Chrome** 88+ (recommended for best performance)
- **Firefox** 85+
- **Safari** 14+
- **Edge** 88+

*Note: Some advanced CSS effects may have reduced functionality on older browsers*

## Performance Considerations

- **Animation Performance**: Uses CSS transforms and opacity for hardware acceleration
- **Bundle Size**: Optimized Vue.js build with tree-shaking
- **Font Loading**: Efficient Google Fonts loading with font-display: swap
- **Image Optimization**: All graphics are CSS-based for scalability
- **Responsive Images**: Adaptive layouts without heavy image assets

## License

This project is open source and available under the MIT License. Feel free to use it as inspiration for your own portfolio projects.

## Credits

- **Design Inspiration**: Classic 8-bit gaming consoles and retro computer terminals
- **Font**: "Press Start 2P" by CodeMan38
- **Framework**: Vue.js team for the excellent framework
- **Build Tool**: Vite team for the lightning-fast development experience

## Contact

For questions, suggestions, or collaboration opportunities regarding this 8-bit portfolio template, feel free to reach out!

---

Built with ❤️ using Vue.js and a passion for retro gaming aesthetics
