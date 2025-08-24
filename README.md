# Math Worksheet

A modern, interactive math worksheet application built with Vue.js, designed to help practice rounding numbers to the nearest 10. The application features a user-friendly interface with real-time feedback and scoring.

## 🎯 Features

-  **Interactive Math Worksheet**: 12 multiple-choice questions on rounding numbers to the nearest 10
-  ** Name Input**: Personalized experience with required name entry
-  **Real-time Validation**: Immediate feedback on form completion and input validation
-  **Scoring System**: Automatic score calculation with encouraging feedback messages
-  **Progress Visualization**: Animated progress bar showing performance
-  **Responsive Design**: Mobile-friendly interface that works on all devices
-  **Modern UI**: Clean, professional design with smooth animations
-  **Reset Functionality**: Option to clear all answers and start over

## 🛠 Tech Stack

-  **Frontend**: [Vue.js 3](https://vuejs.org/) with Composition API
-  **Styling**: [Tailwind CSS](https://tailwindcss.com/) for modern, utility-first styling
-  **Language**: TypeScript for type safety

## 📋 Prerequisites

Before running this application, make sure you have the following installed:

-  [Node.js](https://nodejs.org/) (version 18 or higher)
-  npm or yarn package manager

## 🚀 Quick Start

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd math-worksheet-vue
   ```

2. **Install dependencies**

   ```bash
   npm install
   # or
   yarn install
   ```

3. **Start the development server**

   ```bash
   npm run dev
   # or
   yarn dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:3000` to see the application.

## 📝 Available Scripts

| Command               | Description               |
| --------------------- | ------------------------- |
| `npm run dev`         | Start development server  |
| `npm run build`       | Build for production      |
| `npm run generate`    | Generate static site      |
| `npm run preview`     | Preview production build  |
| `npm run postinstall` | Prepare Nuxt dependencies |

## 🏗 Project Structure

```
math-worksheet-vue/
├── app/
│   ├── app.vue                 # Root application component
│   ├── assets/
│   │   └── css/
│   │       └── main.css        # Global styles and Tailwind components
│   ├── components/
│   │   ├── MathWorksheet.vue   # Main worksheet component
│   │   └── QuestionItem.vue    # Individual question component
│   └── pages/
│       └── index.vue           # Home page
├── nuxt.config.ts              # Nuxt configuration
├── package.json                # Dependencies and scripts
├── tailwind.config.js          # Tailwind CSS configuration
└── tsconfig.json               # TypeScript configuration
```

## 🎮 How to Use

1. **Enter Your Name**: Start by entering your name in the required field
2. **Answer Questions**: Click on the correct answer for each rounding question
3. **Submit**: Once all questions are answered, click "Submit & Get Score"
4. **View Results**: See your score, percentage, and encouraging feedback
5. **Reset (Optional)**: Use "Reset All Answers" to start over

## 📚 Educational Content

The worksheet covers rounding numbers to the nearest 10 with:

-  Numbers from single digits to three digits
-  Various difficulty levels
-  Mixed number patterns to reinforce learning
-  Immediate feedback to support learning

## 🎨 Design Features

-  **Clean Interface**: Minimalist design focusing on content
-  **Responsive Layout**: Works seamlessly on desktop, tablet, and mobile
-  **Visual Feedback**: Color-coded selections and progress indicators
-  **Smooth Animations**: Engaging transitions and hover effects
-  **Accessibility**: Proper contrast ratios and semantic HTML

## 🔧 Configuration

The app is configured with:

-  Tailwind CSS module for styling
-  TypeScript support
-  Development tools enabled
-  Custom app head configuration

### Tailwind Customization

Custom components are defined in `main.css` including:

-  Button styles (primary/secondary)
-  Input field styling
-  Question card layouts
-  Animation classes

## 🌐 Deployment

### Static Generation

```bash
npm run generate
```

This creates a `dist/` folder with static files that can be deployed to any static hosting service.

### Server-Side Rendering

```bash
npm run build
npm run preview
```
