<!DOCTYPE html>
<html lang="en" class="dark scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Markdown to HTML Converter - Live Editor • UtilityKit</title>
  <meta name="description" content="Convert Markdown to HTML with live preview. Write Markdown and instantly see the rendered HTML. Fast, free, and offline Markdown editor.">
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
  <style>
    .copy-feedback { opacity: 0; transition: opacity 0.4s; }
    .copy-feedback.show { opacity: 1; }
    #live-clock { animation: pulse 2s infinite; }
    @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.7; } }
  </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-indigo-50 to-purple-100 dark:from-slate-950 dark:to-slate-900 min-h-screen">

  <!-- Header -->
<header class="bg-white/80 dark:bg-slate-900/80 backdrop-blur-md shadow-lg sticky top-0 z-50">
  <div class="container mx-auto px-6 py-5 flex flex-wrap items-center justify-between">
    <a href="index.html" class="flex items-center gap-3">
      <h1 class="text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600">UtilityKit</h1>
    </a>
    <nav class="flex flex-wrap gap-4 md:gap-6 text-lg">
      <a href="pdf.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-file-pdf mr-1"></i>PDF</a>
      <a href="image.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-image mr-1"></i>Image</a>
      <a href="qr.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-qrcode mr-1"></i>QR</a>
      <a href="ocr.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-eye mr-1"></i>OCR</a>
      <a href="calculator.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-gauge-high mr-1"></i>Calculator</a>
      <a href="password.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-key mr-1"></i>Password</a>
      <a href="json.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-code mr-1"></i>JSON</a>
      <a href="base64.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-lock mr-1"></i>Base64</a>
      <a href="timestamp.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-clock mr-1"></i>Timestamp</a>
      
      <!-- === NEW TOOLS IN NAV === -->
      <a href="compress.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-file-zipper mr-1"></i>Compressor</a>
      <a href="markdown.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-brands fa-markdown mr-1"></i>Markdown</a>
      <a href="currency.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-dollar-sign mr-1"></i>Currency</a>
    </nav>
  </div>
</header><script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
    <!-- Marked.js for fast Markdown parsing -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/marked/12.0.2/marked.min.js"></script>
    <style>
        /* Custom scrollbar for the editors */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }
        .dark ::-webkit-scrollbar-track {
            background: #2d3748; /* slate-800 */
        }
        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 4px;
        }
        .dark ::-webkit-scrollbar-thumb {
            background: #718096; /* slate-600 */
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }

        /* Styling for the HTML output preview pane (to match standard markdown rendering) */
        .html-preview-output {
            padding: 1rem;
            line-height: 1.6;
            word-wrap: break-word;
            overflow-x: hidden;
        }
        .html-preview-output h1, .html-preview-output h2, .html-preview-output h3 {
            font-weight: bold;
            margin-top: 1.5rem;
            margin-bottom: 0.5rem;
            border-bottom: 1px solid #eee;
            padding-bottom: 0.25rem;
        }
        .dark .html-preview-output h1, .dark .html-preview-output h2, .dark .html-preview-output h3 {
            border-bottom-color: #4b5563; /* slate-600 */
        }
        .html-preview-output h1 { font-size: 2.25rem; }
        .html-preview-output h2 { font-size: 1.875rem; }
        .html-preview-output h3 { font-size: 1.5rem; }
        .html-preview-output p { margin-bottom: 1rem; }
        .html-preview-output ul, .html-preview-output ol { margin-left: 1.5rem; margin-bottom: 1rem; }
        .html-preview-output pre {
            background-color: #f4f4ff;
            padding: 1rem;
            border-radius: 0.5rem;
            overflow-x: auto;
            margin-bottom: 1rem;
            font-size: 0.875rem;
            white-space: pre-wrap;
        }
        .dark .html-preview-output pre {
            background-color: #1f2937; /* gray-800 */
        }
        .html-preview-output code {
            background-color: #e2e8f0; /* slate-200 */
            padding: 0.2em 0.4em;
            margin: 0;
            border-radius: 6px;
            font-size: 85%;
        }
        .dark .html-preview-output code {
            background-color: #374151; /* gray-700 */
        }
        .html-preview-output blockquote {
            border-left: 4px solid #4f46e5; /* indigo-600 */
            padding-left: 1rem;
            margin: 1rem 0;
            color: #4b5563;
        }
        .dark .html-preview-output blockquote {
            color: #9ca3af; /* gray-400 */
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-indigo-50 to-purple-100 dark:from-slate-950 dark:to-slate-900 min-h-screen font-sans text-gray-900 dark:text-gray-100">

    <div class="container mx-auto px-4 py-8 max-w-7xl">
        <!-- Header -->
        <div class="text-center mb-10">
            
            <h1 class="text-5xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 mb-2">
                Markdown to HTML Live Editor
            </h1>
            <p class="text-xl text-slate-600 dark:text-slate-400">
                Write Markdown and see the rendered HTML instantly.
            </p>
        </div>

        <div class="bg-white dark:bg-slate-800 rounded-xl shadow-2xl p-6 lg:p-8">
            <!-- Action Buttons -->
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-6 pb-4 border-b dark:border-slate-700">
                <div id="statusMessage" class="text-sm font-medium text-green-600 dark:text-green-400 opacity-0 transition-opacity duration-300"></div>
                <div class="flex gap-4">
                    <button id="copyHtmlButton" class="flex items-center px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-lg shadow-md transition duration-150">
                        <i class="fa-solid fa-copy mr-2"></i> Copy HTML
                    </button>
                    <button id="downloadHtmlButton" class="flex items-center px-4 py-2 bg-purple-600 hover:bg-purple-700 text-white font-semibold rounded-lg shadow-md transition duration-150">
                        <i class="fa-solid fa-download mr-2"></i> Download HTML
                    </button>
                </div>
            </div>

            <!-- Split Pane Editor -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 h-[70vh] min-h-[500px]">
                <!-- Markdown Editor Panel -->
                <div class="flex flex-col">
                    <h2 class="text-lg font-semibold mb-2 text-indigo-600 dark:text-indigo-400 flex justify-between items-center">
                        Markdown Source
                        <button id="showGuideButton" class="text-xs text-slate-500 hover:text-slate-700 dark:hover:text-slate-300 transition duration-150">
                            <i class="fa-solid fa-question-circle mr-1"></i> Guide
                        </button>
                    </h2>
                    <textarea id="markdownInput" placeholder="Start typing your Markdown here..."
                        class="flex-grow w-full p-4 border border-slate-300 dark:border-slate-700 rounded-lg resize-none focus:ring-indigo-500 focus:border-indigo-500 dark:bg-slate-900 dark:text-gray-200 outline-none shadow-inner text-sm leading-relaxed font-mono"
                        spellcheck="false"></textarea>
                </div>

                <!-- HTML Preview Panel -->
                <div class="flex flex-col">
                    <h2 class="text-lg font-semibold mb-2 text-purple-600 dark:text-purple-400">
                        HTML Live Preview
                    </h2>
                    <div id="htmlPreview" class="flex-grow w-full border border-slate-300 dark:border-slate-700 rounded-lg overflow-y-auto bg-slate-50 dark:bg-slate-900 html-preview-output shadow-inner">
                        <!-- Rendered HTML will go here -->
                        <p class="text-slate-500 dark:text-slate-400">Start typing in the Markdown editor to see the live HTML preview here.</p>
                    </div>
                </div>
            </div>

            <!-- Markdown Guide (Hidden by default) -->
            <div id="markdownGuide" class="mt-8 p-6 bg-slate-100 dark:bg-slate-900 rounded-lg border border-slate-300 dark:border-slate-700 hidden transition-all duration-300">
                <h3 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Basic Markdown Cheat Sheet</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 text-sm">
                    <div>
                        <p class="font-semibold text-gray-700 dark:text-gray-300">Headings:</p>
                        <ul class="list-disc list-inside ml-2">
                            <li><code># H1</code></li>
                            <li><code>## H2</code></li>
                            <li><code>### H3</code></li>
                        </ul>
                    </div>
                    <div>
                        <p class="font-semibold text-gray-700 dark:text-gray-300">Text Styling:</p>
                        <ul class="list-disc list-inside ml-2">
                            <li>Bold: <code>**text**</code> or <code>__text__</code></li>
                            <li>Italic: <code>*text*</code> or <code>_text_</code></li>
                            <li>Code (Inline): <code>`code`</code></li>
                        </ul>
                    </div>
                    <div>
                        <p class="font-semibold text-gray-700 dark:text-gray-300">Lists:</p>
                        <ul class="list-disc list-inside ml-2">
                            <li>Unordered: <code>* Item</code> or <code>- Item</code></li>
                            <li>Ordered: <code>1. Item</code></li>
                        </ul>
                    </div>
                    <div>
                        <p class="font-semibold text-gray-700 dark:text-gray-300">Links & Images:</p>
                        <ul class="list-disc list-inside ml-2">
                            <li>Link: <code>[Text](URL)</code></li>
                            <li>Image: <code>![Alt Text](URL)</code></li>
                        </ul>
                    </div>
                </div>
            </div>

        </div>
    </div>

    <!-- JavaScript Logic -->
    <script>
        const markdownInput = document.getElementById('markdownInput');
        const htmlPreview = document.getElementById('htmlPreview');
        const copyHtmlButton = document.getElementById('copyHtmlButton');
        const downloadHtmlButton = document.getElementById('downloadHtmlButton');
        const showGuideButton = document.getElementById('showGuideButton');
        const markdownGuide = document.getElementById('markdownGuide');
        const statusMessage = document.getElementById('statusMessage');

        // Set initial Markdown content
        const initialMarkdown = `# Welcome to the Live Markdown Editor

This tool allows you to instantly convert Markdown to HTML.

## Features
1.  **Split-Pane:** Write Markdown on the left, see HTML on the right.
2.  **Live Preview:** Updates as you type.
3.  **Copy/Download:** Get the raw HTML output.

### Basic Formatting
-   *Italic* and **Bold** text are supported.
-   [Links](https://example.com) work too!

\`\`\`javascript
// Code blocks are also supported!
function helloWorld() {
    console.log("Hello, World!");
}
\`\`\`
> "Markdown is a lightweight markup language that allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid HTML."
`;

        markdownInput.value = initialMarkdown;

        /**
         * Converts the Markdown input to HTML and updates the preview pane.
         */
        function updatePreview() {
            const markdownText = markdownInput.value;
            // Use marked.js to convert Markdown to HTML
            const html = marked.parse(markdownText);
            htmlPreview.innerHTML = html;
        }

        /**
         * Shows a temporary status message (e.g., "Copied!")
         * @param {string} message The message to display.
         * @param {string} type The color type ('success' or 'error').
         */
        function showStatus(message, type = 'success') {
            statusMessage.textContent = message;
            statusMessage.classList.remove('opacity-0', 'text-green-600', 'text-red-600', 'dark:text-green-400', 'dark:text-red-400');
            if (type === 'success') {
                statusMessage.classList.add('text-green-600', 'dark:text-green-400');
            } else if (type === 'error') {
                statusMessage.classList.add('text-red-600', 'dark:text-red-400');
            }
            statusMessage.classList.add('opacity-100');

            setTimeout(() => {
                statusMessage.classList.remove('opacity-100');
                statusMessage.classList.add('opacity-0');
            }, 3000);
        }

        // --- Event Listeners and Initial Load ---

        // 1. Live Update on Input
        markdownInput.addEventListener('input', updatePreview);

        // 2. Copy HTML Functionality
        copyHtmlButton.addEventListener('click', () => {
            const htmlOutput = htmlPreview.innerHTML;
            // Use document.execCommand('copy') for better compatibility in sandboxed environments
            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = htmlOutput;
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            try {
                const successful = document.execCommand('copy');
                if (successful) {
                    showStatus('HTML copied to clipboard!');
                } else {
                    showStatus('Failed to copy. Please copy manually.', 'error');
                }
            } catch (err) {
                console.error('Copy failed:', err);
                showStatus('Copy failed (Browser restriction).', 'error');
            }
            document.body.removeChild(tempTextArea);
        });

        // 3. Download HTML File Functionality
        downloadHtmlButton.addEventListener('click', () => {
            const htmlContent = htmlPreview.innerHTML;
            const fileContent = `<!DOCTYPE html>\n<html lang="en">\n<head>\n  <meta charset="UTF-8">\n  <meta name="viewport" content="width=device-width, initial-scale=1.0">\n  <title>Rendered Markdown</title>\n</head>\n<body>\n${htmlContent}\n</body>\n</html>`;

            const blob = new Blob([fileContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'markdown_output.html';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            showStatus('HTML file downloaded!');
        });

        // 4. Toggle Markdown Guide
        showGuideButton.addEventListener('click', () => {
            if (markdownGuide.classList.contains('hidden')) {
                markdownGuide.classList.remove('hidden');
                showGuideButton.textContent = 'Hide Guide';
            } else {
                markdownGuide.classList.add('hidden');
                showGuideButton.textContent = 'Guide';
            }
        });

        // 5. Initial Run
        updatePreview();

    </script>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const currentPage = location.pathname.split('/').pop() || 'index.html';

    document.querySelectorAll('.nav-link').forEach(link => {
      if (link.getAttribute('href') === currentPage) {
        link.classList.add('text-indigo-600', 'font-bold');
        link.classList.remove('text-slate-700', 'dark:text-slate-300', 'hover:text-indigo-600');
      } else {
        link.classList.add('text-slate-700', 'dark:text-slate-300', 'hover:text-indigo-600');
      }
    });
  });
</script>
</body>
</html>
