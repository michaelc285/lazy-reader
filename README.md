# Lazy Reader

Lazy Reader is a web-based speed reading tool designed exclusively for Chinese text, helping users read efficiently by displaying words one at a time. Built with SvelteKit, TypeScript, and pure CSS, it offers a clean, responsive interface optimized for both desktop and mobile devices, ideal for reading Chinese articles, study materials, or literature.

## Features

- **Chinese Text Input**: Enter Chinese text of any length with no word limit.
- **Punctuation Toggle**: Option to keep or remove Chinese punctuation (e.g., 。, ，, ！) during playback.
- **Word-by-Word Playback**: Displays one Chinese character or word at a time at a customizable speed (100–1000 words per minute, default 500).

## Use Cases

- **Reading Practice**: Improve Chinese reading speed with articles or books.
- **Study Aid**: Break down dense Chinese study materials into manageable chunks.
- **Language Learning**: Enhance comprehension by focusing on individual characters or words.

## Getting Started

### Prerequisites

- Node.js (v18 or higher)
- pnpm (v8 or higher)

### Installation

Clone the repository:
```bash
   git clone git@github.com:michaelc285/lazy-reader.git
   cd lazy-reader
```

Install dependencies:
```bash
pnpm install
```

Start the development server:
```bash
pnpm dev
```

Open http://localhost:5173 in your browser to view the app.


Build for Production

Build the project:
```bash
pnpm build
```

Deploy:
```bash
pnpm run deploy
```