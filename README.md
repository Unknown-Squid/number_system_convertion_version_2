# Number System Conversion

A modern, single-page Vue.js application for converting numbers between different number systems: Decimal, Binary, Hexadecimal, and Octal.

## Features

- 🎨 **Beautiful UI** - Modern design with animated background video
- 🔄 **Multi-base Conversion** - Convert between Decimal, Binary, Hexadecimal, and Octal
- 📱 **Responsive Design** - Works seamlessly on desktop and mobile devices
- ⚡ **Fast & Lightweight** - Built with Vue 3 and Vite for optimal performance
- 🎯 **One-page Layout** - No scrolling required, everything fits on one screen
- 🎬 **Animated Background** - Blurred video background with overlay effects

## Number Systems Supported

- **Decimal** (Base 10) - Standard number system (0-9)
- **Binary** (Base 2) - Computer number system (0-1)
- **Hexadecimal** (Base 16) - Common in programming (0-9, A-F)
- **Octal** (Base 8) - Used in some computing contexts (0-7)

## Getting Started

### Prerequisites

- **Node.js** (v20.19.0 or >=22.12.0 recommended) - Required to run the development server, build tools (Vite), and manage dependencies via npm
- **npm** or **yarn** - Package managers (npm comes bundled with Node.js)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd number_system_convertion_version_2
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```
```

## Usage

1. Click on one of the four conversion boxes (Decimal, Binary, Hexadecimal, or Octal)
2. Enter the value you want to convert in the input field
3. Select the target number system from the dropdown menu
4. Click the "Convert" button to see the result

## Project Structure

```
number_system_convertion_version_2/
├── public/
│   ├── animations/
│   │   └── Number_System_Conversion_Animation.mp4
│   └── number-conversion-icon.svg
├── src/
│   ├── App.vue          # Main application component
│   ├── main.ts          # Application entry point
│   ├── style.css        # Global styles
│   └── vue-shim.d.ts    # TypeScript declarations for Vue components
├── index.html
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## Technologies Used

- **Vue 3** - Progressive JavaScript framework
- **TypeScript** - Type-safe JavaScript
- **Vite** - Next-generation frontend build tool
- **CSS3** - Modern styling with animations and effects

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Author
Gerald Fegalan
Created with ❤️ for number system conversions
