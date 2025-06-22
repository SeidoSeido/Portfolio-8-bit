# Frontend Developer Portfolio

A modern, interactive portfolio website built with Vue.js showcasing the work and skills of a seasoned frontend developer.

## Features

- **Interactive Landing Page**: Features your name on the left and a fun "Catch the Stars" mini-game on the right
- **Responsive Design**: Fully responsive across all devices
- **Modern UI/UX**: Clean, professional design with smooth animations
- **Skills Showcase**: Interactive skill bars with progress indicators
- **Project Portfolio**: Filterable project gallery with hover effects
- **Contact Form**: Functional contact form with validation
- **Performance Optimized**: Built with Vite for fast development and optimized builds

## Technologies Used

- **Vue.js 3** - Progressive JavaScript framework
- **Vite** - Fast build tool and dev server
- **CSS3** - Modern styling with CSS Grid and Flexbox
- **HTML5** - Semantic markup
- **JavaScript ES6+** - Modern JavaScript features

## Getting Started

### Prerequisites

- Node.js (version 14 or higher)
- npm or yarn

### Installation

1. Clone the repository or download the files
2. Navigate to the project directory:
   ```bash
   cd PortfolioMain
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

5. Open your browser and visit `http://localhost:3000`

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
│   ├── Navigation.vue      # Navigation bar with mobile menu
│   ├── HeroSection.vue     # Landing section with mini-game
│   ├── AboutSection.vue    # About section with stats
│   ├── SkillsSection.vue   # Skills and certifications
│   ├── ProjectsSection.vue # Project portfolio with filtering
│   └── ContactSection.vue  # Contact form and information
├── App.vue                 # Main application component
├── main.js                 # Application entry point
└── style.css              # Global styles

```

## Customization

### Personal Information

Update the following components with your personal information:

1. **HeroSection.vue**: Change name, title, and description
2. **AboutSection.vue**: Update about text and statistics
3. **SkillsSection.vue**: Modify skills and certifications
4. **ProjectsSection.vue**: Add your actual projects
5. **ContactSection.vue**: Update contact information

### Styling

- Global styles are in `src/style.css`
- Component-specific styles are in each Vue component's `<style>` section
- Color scheme can be easily changed by updating CSS custom properties

### Mini-Game

The "Catch the Stars" mini-game in the hero section includes:
- Mouse-controlled paddle
- Falling stars to catch
- Score tracking
- Timer (30 seconds)
- Responsive design

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This project is open source and available under the MIT License.

## Contact

For questions or suggestions about this portfolio template, feel free to reach out!

---

Built with ❤️ using Vue.js
