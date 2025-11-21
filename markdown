<!DOCTYPE html>
<html lang="en" class="dark scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Developer Tools & Markdown • UtilityKit</title>
  <meta name="description" content="Markdown Editor, Code Formatter, Diff Checker, and Regex Tester. 100% Client-side.">
  
  <!-- Tailwind & Icons -->
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
  
  <!-- Monaco Editor Loader -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/monaco-editor/0.46.0/min/vs/loader.min.js"></script>
  <!-- Markdown Parser (Marked.js) -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

  <style>
    /* Custom Scrollbar to match theme */
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-track { background: rgba(30, 41, 59, 0.5); }
    ::-webkit-scrollbar-thumb { background: #4b5563; border-radius: 4px; }
    ::-webkit-scrollbar-thumb:hover { background: #6b7280; }

    /* Editor Containers */
    .editor-container { height: 500px; border-radius: 0.75rem; overflow: hidden; border: 1px solid #334155; }
    .diff-editor-container { height: 600px; border-radius: 0.75rem; overflow: hidden; border: 1px solid #334155; }
    
    /* Preview Area */
    .preview-content { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; line-height: 1.6; }
    .preview-content h1 { font-size: 2em; font-weight: bold; margin-bottom: 0.5em; border-bottom: 1px solid #475569; padding-bottom: 0.2em; }
    .preview-content h2 { font-size: 1.5em; font-weight: bold; margin-top: 1em; margin-bottom: 0.5em; }
    .preview-content p { margin-bottom: 1em; }
    .preview-content code { background-color: rgba(99, 102, 241, 0.1); padding: 0.2em 0.4em; border-radius: 0.25em; font-family: monospace; color: #818cf8; }
    .preview-content pre { background-color: #1e293b; padding: 1em; border-radius: 0.5em; overflow-x: auto; margin-bottom: 1em; }
    .preview-content pre code { background-color: transparent; color: #e2e8f0; padding: 0; }
    .preview-content blockquote { border-left: 4px solid #6366f1; padding-left: 1em; margin-left: 0; color: #94a3b8; font-style: italic; }
    .preview-content ul { list-style-type: disc; padding-left: 1.5em; margin-bottom: 1em; }
    .preview-content ol { list-style-type: decimal; padding-left: 1.5em; margin-bottom: 1em; }
    .preview-content a { color: #6366f1; text-decoration: underline; }

    /* Tab Active State */
    .tab-btn.active { background-color: rgba(99, 102, 241, 0.1); color: #818cf8; border-bottom: 2px solid #818cf8; }

    /* Regex Highlights */
    .highlight-match { background-color: rgba(250, 204, 21, 0.4); border-bottom: 2px solid #facc15; color: white; padding: 0 2px; border-radius: 2px; }
  </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-indigo-50 to-purple-100 dark:from-slate-950 dark:to-slate-900 min-h-screen flex flex-col">

<!-- Header (Matches index.html) -->
<header class="bg-white/80 dark:bg-slate-900/80 backdrop-blur-md shadow-lg sticky top-0 z-50">
  <div class="container mx-auto px-6 py-5 flex flex-wrap items-center justify-between">
    <a href="index.html" class="flex items-center gap-3">
      <h1 class="text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600">UtilityKit</h1>
    </a>
    <nav class="flex flex-wrap gap-4 md:gap-6 text-lg">
      <a href="pdf.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-file-pdf mr-1"></i>PDF</a>
      <a href="image.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-image mr-1"></i>Image</a>
      <a href="compress.html" class="nav-link hover:text-blue-600 dark:hover:text-blue-400 transition"><i class="fa-solid fa-file-zipper mr-1"></i>Compressor</a>
      <!-- Active Page -->
      <a href="markdown.html" class="nav-link text-blue-600 dark:text-blue-400 font-bold transition"><i class="fa-solid fa-code mr-1"></i>DevTools</a>
    </nav>
  </div>
</header>

<div class="container mx-auto px-4 md:px-6 py-12 max-w-7xl flex-grow">
    
    <!-- Title Section -->
    <div class="text-center mb-10">
      <h1 class="text-5xl md:text-6xl font-black text-transparent bg-clip-text bg-gradient-to-r from-indigo-500 to-teal-400 mb-4">
        Developer Studio
      </h1>
      <p class="text-xl text-slate-600 dark:text-slate-400">Markdown Editor • Code Formatter • Diff Checker • Regex Tester</p>
    </div>

    <!-- Navigation Tabs -->
    <div class="bg-white dark:bg-slate-800 p-2 rounded-2xl shadow-lg mb-8 flex flex-wrap justify-center gap-2 border border-slate-200 dark:border-slate-700">
        <button class="tab-btn active flex-1 min-w-[120px] px-4 py-3 rounded-xl text-sm font-bold text-slate-500 hover:text-indigo-500 hover:bg-slate-100 dark:hover:bg-slate-700 transition-all" data-target="markdown">
            <i class="fa-brands fa-markdown mr-2 text-lg"></i>Markdown
        </button>
        <button class="tab-btn flex-1 min-w-[120px] px-4 py-3 rounded-xl text-sm font-bold text-slate-500 hover:text-indigo-500 hover:bg-slate-100 dark:hover:bg-slate-700 transition-all" data-target="formatter">
            <i class="fas fa-align-left mr-2 text-lg"></i>Formatter
        </button>
        <button class="tab-btn flex-1 min-w-[120px] px-4 py-3 rounded-xl text-sm font-bold text-slate-500 hover:text-indigo-500 hover:bg-slate-100 dark:hover:bg-slate-700 transition-all" data-target="diff-checker">
            <i class="fas fa-columns mr-2 text-lg"></i>Diff Check
        </button>
        <button class="tab-btn flex-1 min-w-[120px] px-4 py-3 rounded-xl text-sm font-bold text-slate-500 hover:text-indigo-500 hover:bg-slate-100 dark:hover:bg-slate-700 transition-all" data-target="regex-tester">
            <i class="fas fa-flask mr-2 text-lg"></i>Regex
        </button>
    </div>

    <!-- CONTENT: MARKDOWN EDITOR -->
    <div id="markdown" class="tool-content">
        <div class="bg-white dark:bg-slate-800 rounded-3xl shadow-2xl border border-slate-200 dark:border-slate-700 overflow-hidden">
            <!-- Toolbar -->
            <div class="bg-slate-100 dark:bg-slate-900 p-3 border-b border-slate-200 dark:border-slate-700 flex justify-between items-center">
                <div class="flex gap-2">
                    <span class="text-sm font-bold text-slate-500 px-3 py-1">Editor</span>
                </div>
                <div class="flex gap-2">
                    <button id="md-download-btn" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white text-sm font-bold rounded-lg transition shadow-lg shadow-indigo-500/30">
                        <i class="fas fa-download mr-2"></i>Save .md
                    </button>
                    <button id="html-export-btn" class="px-4 py-2 bg-teal-600 hover:bg-teal-700 text-white text-sm font-bold rounded-lg transition shadow-lg shadow-teal-500/30">
                        <i class="fas fa-code mr-2"></i>Export HTML
                    </button>
                </div>
            </div>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 h-[600px]">
                <!-- Editor Pane -->
                <div id="markdown-editor-container" class="h-full border-r border-slate-200 dark:border-slate-700 bg-[#1e1e1e]"></div>
                
                <!-- Preview Pane -->
                <div id="markdown-preview" class="h-full p-8 overflow-y-auto bg-white dark:bg-slate-800 text-slate-800 dark:text-slate-200 preview-content">
                    <h1 class="text-center text-gray-400 mt-20">Preview will appear here...</h1>
                </div>
            </div>
        </div>
    </div>

    <!-- CONTENT: FORMATTER -->
    <div id="formatter" class="tool-content hidden">
        <div class="bg-white dark:bg-slate-800 rounded-3xl shadow-2xl p-6 border border-slate-200 dark:border-slate-700">
            <div class="flex flex-wrap items-center justify-between gap-4 mb-4">
                <h2 class="text-2xl font-bold text-slate-700 dark:text-white"><i class="fas fa-magic mr-2 text-indigo-500"></i>Code Beautifier</h2>
                <select id="language-select" class="bg-slate-100 dark:bg-slate-700 border-none text-slate-800 dark:text-white text-sm rounded-xl focus:ring-2 focus:ring-indigo-500 block p-3 min-w-[150px] font-bold">
                    <option value="json">JSON</option>
                    <option value="javascript">JavaScript</option>
                    <option value="html">HTML</option>
                    <option value="css">CSS</option>
                    <option value="sql">SQL</option>
                    <option value="xml">XML</option>
                </select>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div>
                    <label class="text-xs font-bold text-slate-500 uppercase mb-2 block ml-1">Input Code</label>
                    <div id="fmt-input-container" class="editor-container shadow-inner"></div>
                </div>
                <div>
                    <label class="text-xs font-bold text-slate-500 uppercase mb-2 block ml-1">Beautified Output</label>
                    <div id="fmt-output-container" class="editor-container shadow-inner"></div>
                </div>
            </div>

            <div class="mt-6 flex flex-wrap gap-3 justify-end">
                <button id="format-btn" class="px-8 py-3 bg-gradient-to-r from-indigo-500 to-blue-600 hover:from-indigo-600 hover:to-blue-700 text-white font-bold rounded-xl transition shadow-lg flex items-center">
                    <i class="fas fa-align-left mr-2"></i> Beautify
                </button>
                <button id="minify-btn" class="px-8 py-3 bg-slate-700 hover:bg-slate-600 text-white font-bold rounded-xl transition flex items-center">
                    <i class="fas fa-compress mr-2"></i> Minify
                </button>
                <button id="copy-fmt-btn" class="px-8 py-3 bg-emerald-500 hover:bg-emerald-600 text-white font-bold rounded-xl transition shadow-lg flex items-center">
                    <i class="fas fa-copy mr-2"></i> Copy
                </button>
            </div>
            <div id="fmt-message" class="mt-3 text-center text-sm text-red-500 hidden font-bold"></div>
        </div>
    </div>

    <!-- CONTENT: DIFF CHECKER -->
    <div id="diff-checker" class="tool-content hidden">
        <div class="bg-white dark:bg-slate-800 rounded-3xl shadow-2xl p-6 border border-slate-200 dark:border-slate-700">
            <div class="flex items-center justify-between mb-4">
                <h2 class="text-2xl font-bold text-slate-700 dark:text-white"><i class="fas fa-columns mr-2 text-purple-500"></i>Diff Checker</h2>
                <div class="flex gap-2">
                    <button id="diff-sample-btn" class="text-xs font-bold bg-slate-200 dark:bg-slate-700 hover:bg-slate-300 dark:hover:bg-slate-600 px-4 py-2 rounded-lg transition">Load Sample</button>
                    <button id="diff-layout-toggle" class="text-xs font-bold bg-slate-200 dark:bg-slate-700 hover:bg-slate-300 dark:hover:bg-slate-600 px-4 py-2 rounded-lg transition">Inline / Split</button>
                </div>
            </div>

            <div id="diff-editor-container" class="diff-editor-container shadow-inner bg-[#1e1e1e]"></div>
            
            <p class="mt-4 text-center text-sm text-slate-500 font-medium">
                <i class="fas fa-info-circle mr-1"></i> Paste text directly into the left (Original) and right (Modified) panes.
            </p>
        </div>
    </div>

    <!-- CONTENT: REGEX TESTER -->
    <div id="regex-tester" class="tool-content hidden">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Main Tester -->
            <div class="lg:col-span-2">
                <div class="bg-white dark:bg-slate-800 rounded-3xl shadow-2xl p-6 border border-slate-200 dark:border-slate-700 h-full">
                    <h2 class="text-2xl font-bold text-slate-700 dark:text-white mb-6"><i class="fas fa-flask mr-2 text-pink-500"></i>Regex Tester</h2>

                    <!-- Regex Input -->
                    <div class="bg-slate-100 dark:bg-slate-900 p-4 rounded-xl border border-slate-200 dark:border-slate-700 mb-4 flex items-center gap-2 shadow-inner">
                        <span class="text-slate-400 font-mono text-lg">/</span>
                        <input type="text" id="regex-input" placeholder="Expression..." class="bg-transparent border-none text-slate-800 dark:text-white w-full focus:ring-0 font-mono text-lg placeholder-slate-400" value="([A-Z])\w+">
                        <span class="text-slate-400 font-mono text-lg">/</span>
                        <input type="text" id="regex-flags" placeholder="gim" class="bg-transparent border-none text-indigo-500 w-16 focus:ring-0 font-mono text-lg font-bold" value="g">
                    </div>

                    <!-- Test String -->
                    <div class="mb-4">
                        <label class="text-xs font-bold text-slate-500 uppercase mb-2 block">Test String</label>
                        <textarea id="regex-text-input" class="w-full h-40 bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl p-4 font-mono text-sm text-slate-800 dark:text-slate-300 focus:ring-2 focus:ring-indigo-500 outline-none resize-none" placeholder="Paste text here...">The Quick Brown Fox Jumps Over The Lazy Dog.</textarea>
                    </div>

                    <!-- Output -->
                    <div>
                        <div class="flex justify-between items-end mb-2">
                            <label class="text-xs font-bold text-slate-500 uppercase">Match Result</label>
                            <span id="match-count" class="text-xs font-bold text-white bg-slate-400 px-3 py-1 rounded-full">0 Matches</span>
                        </div>
                        <div id="regex-output" class="w-full min-h-[160px] max-h-[300px] overflow-y-auto bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl p-4 font-mono text-sm text-slate-600 dark:text-slate-400 whitespace-pre-wrap"></div>
                    </div>
                </div>
            </div>

            <!-- Cheatsheet -->
            <div class="lg:col-span-1">
                <div class="bg-white dark:bg-slate-800 rounded-3xl shadow-xl p-6 border border-slate-200 dark:border-slate-700 sticky top-24">
                    <h3 class="text-lg font-bold mb-4 text-slate-700 dark:text-slate-300"><i class="fas fa-book mr-2"></i>Cheatsheet</h3>
                    <div class="space-y-2 text-sm text-slate-600 dark:text-slate-400 font-mono">
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">.</span> <span>Any char</span></div>
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">\w</span> <span>Word char</span></div>
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">\d</span> <span>Digit</span></div>
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">[abc]</span> <span>Any of a,b,c</span></div>
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">^</span> <span>Start of line</span></div>
                        <div class="flex justify-between"><span class="text-indigo-500 font-bold">$</span> <span>End of line</span></div>
                        <hr class="border-slate-200 dark:border-slate-700 my-2">
                        <div class="flex justify-between"><span class="text-pink-500 font-bold">*</span> <span>0 or more</span></div>
                        <div class="flex justify-between"><span class="text-pink-500 font-bold">+</span> <span>1 or more</span></div>
                        <div class="flex justify-between"><span class="text-pink-500 font-bold">?</span> <span>0 or 1</span></div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="text-center mt-20 text-slate-600 dark:text-slate-400">
      <p class="text-xl">© 2025 UtilityKit • Made with <span class="text-red-500">♥</span> for privacy</p>
    </footer>
</div>

<script>
    // Monaco Environment Setup
    require.config({ paths: { 'vs': 'https://cdnjs.cloudflare.com/ajax/libs/monaco-editor/0.46.0/min/vs' } });
    window.MonacoEnvironment = { getWorkerUrl: () => proxy };
    let proxy = URL.createObjectURL(new Blob(['self.MonacoEnvironment = { baseUrl: "https://cdnjs.cloudflare.com/ajax/libs/monaco-editor/0.46.0/min/" }; importScripts("https://cdnjs.cloudflare.com/ajax/libs/monaco-editor/0.46.0/min/vs/base/worker/workerMain.min.js");'], { type: 'text/javascript' }));

    // Global Editor Instances
    let mdEditor, fmtInput, fmtOutput, diffEditor;

    require(["vs/editor/editor.main"], function () {
        initMarkdownEditor();
        initFormatter();
        initDiffChecker();
        initTabs();
        initRegex();
    });

    // --- 1. MARKDOWN EDITOR ---
    function initMarkdownEditor() {
        const container = document.getElementById('markdown-editor-container');
        const preview = document.getElementById('markdown-preview');
        const initialMd = "# Hello UtilityKit!\n\nStart typing markdown on the left.\n\n- [x] Live Preview\n- [x] Syntax Highlighting\n- [x] Export to HTML\n\n```javascript\nconsole.log('Code blocks supported');\n```";

        mdEditor = monaco.editor.create(container, {
            value: initialMd,
            language: 'markdown',
            theme: 'vs-dark',
            minimap: { enabled: false },
            automaticLayout: true,
            wordWrap: 'on',
            padding: { top: 20 }
        });

        // Live Update
        const updatePreview = () => {
            const md = mdEditor.getValue();
            preview.innerHTML = marked.parse(md);
        };

        mdEditor.onDidChangeModelContent(updatePreview);
        updatePreview(); // Initial call

        // Download Buttons
        document.getElementById('md-download-btn').addEventListener('click', () => downloadFile('document.md', mdEditor.getValue(), 'text/markdown'));
        document.getElementById('html-export-btn').addEventListener('click', () => {
            const html = `<!DOCTYPE html><html><body style="font-family:sans-serif;max-width:800px;margin:0 auto;padding:20px;">${marked.parse(mdEditor.getValue())}</body></html>`;
            downloadFile('document.html', html, 'text/html');
        });
    }

    // --- 2. FORMATTER ---
    function initFormatter() {
        fmtInput = monaco.editor.create(document.getElementById('fmt-input-container'), {
            value: '{"name":"UtilityKit","tools":["Markdown","Diff"]}',
            language: 'json',
            theme: 'vs-dark',
            minimap: { enabled: false },
            automaticLayout: true
        });

        fmtOutput = monaco.editor.create(document.getElementById('fmt-output-container'), {
            value: '',
            language: 'json',
            theme: 'vs-dark',
            readOnly: true,
            minimap: { enabled: false },
            automaticLayout: true
        });

        document.getElementById('language-select').addEventListener('change', (e) => {
            const lang = e.target.value;
            monaco.editor.setModelLanguage(fmtInput.getModel(), lang);
            monaco.editor.setModelLanguage(fmtOutput.getModel(), lang);
        });

        document.getElementById('format-btn').addEventListener('click', () => processFormat(true));
        document.getElementById('minify-btn').addEventListener('click', () => processFormat(false));
        
        document.getElementById('copy-fmt-btn').addEventListener('click', () => {
            navigator.clipboard.writeText(fmtOutput.getValue()).then(() => alert('Copied to clipboard!'));
        });
    }

    function processFormat(pretty) {
        const code = fmtInput.getValue();
        const lang = document.getElementById('language-select').value;
        const msg = document.getElementById('fmt-message');
        msg.classList.add('hidden');

        try {
            let res = '';
            if (lang === 'json') {
                const o = JSON.parse(code);
                res = pretty ? JSON.stringify(o, null, 2) : JSON.stringify(o);
            } else {
                // Basic fallback formatting logic for demo
                // In production, integrate Prettier or js-beautify here
                if (pretty) {
                     res = code.replace(/>\s*</g, ">\n<").trim(); // Very basic HTML/XML indent hack
                } else {
                     res = code.replace(/\s+/g, ' ').trim();
                }
                if(lang === 'javascript' && pretty) {
                    // Basic bracket format hack
                    res = code.replace(/{/g, '{\n  ').replace(/}/g, '\n}').replace(/;/g, ';\n');
                }
            }
            fmtOutput.setValue(res);
        } catch (e) {
            msg.textContent = "Error: " + e.message;
            msg.classList.remove('hidden');
        }
    }

    // --- 3. DIFF CHECKER ---
    function initDiffChecker() {
        diffEditor = monaco.editor.createDiffEditor(document.getElementById('diff-editor-container'), {
            theme: 'vs-dark',
            automaticLayout: true,
            originalEditable: true
        });

        const model1 = monaco.editor.createModel("The quick brown fox jumps over the lazy dog.", "text/plain");
        const model2 = monaco.editor.createModel("The quick red fox jumps over the sleepy cat.", "text/plain");

        diffEditor.setModel({ original: model1, modified: model2 });

        document.getElementById('diff-layout-toggle').addEventListener('click', () => {
             const current = diffEditor.getOption(monaco.editor.EditorOption.renderSideBySide);
             diffEditor.updateOptions({ renderSideBySide: !current });
        });

        document.getElementById('diff-sample-btn').addEventListener('click', () => {
            model1.setValue("function hello() {\n  console.log('world');\n}");
            model2.setValue("function hello() {\n  console.log('utility kit');\n  return true;\n}");
            monaco.editor.setModelLanguage(model1, 'javascript');
            monaco.editor.setModelLanguage(model2, 'javascript');
        });
    }

    // --- 4. REGEX TESTER ---
    function initRegex() {
        const input = document.getElementById('regex-input');
        const flags = document.getElementById('regex-flags');
        const text = document.getElementById('regex-text-input');
        const output = document.getElementById('regex-output');
        const countEl = document.getElementById('match-count');

        const run = () => {
            try {
                if(!input.value) { output.innerText = text.value; countEl.innerText = "0 Matches"; countEl.className="text-xs font-bold text-slate-500 bg-slate-200 px-3 py-1 rounded-full"; return; }
                
                const re = new RegExp(input.value, flags.value);
                const str = text.value;
                let matchCount = 0;

                // Simple highlight logic
                // Note: For robust highlighting, we need to avoid breaking HTML. 
                // We will escape HTML first, then apply span tags.
                const escaped = str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
                
                // We can't easily use regex on already escaped string if regex expects chars that were escaped.
                // Simplified approach: Use replace on raw string with callback, but ensure we escape the chunks.
                
                // Re-creating regex with 'g' to count matches if not present
                const globalRe = new RegExp(input.value, flags.value.includes('g') ? flags.value : flags.value + 'g');
                const matches = [...str.matchAll(globalRe)];
                matchCount = matches.length;

                // Construct HTML
                let lastIdx = 0;
                let html = "";
                
                matches.forEach(m => {
                    const pre = str.substring(lastIdx, m.index);
                    const matchVal = m[0];
                    html += escapeHtml(pre) + `<span class="highlight-match">${escapeHtml(matchVal)}</span>`;
                    lastIdx = m.index + matchVal.length;
                    if(!flags.value.includes('g')) lastIdx = str.length; // Stop after one if not global
                });
                html += escapeHtml(str.substring(lastIdx));

                output.innerHTML = html;
                countEl.innerText = `${matchCount} Matches`;
                countEl.className = matchCount > 0 ? "text-xs font-bold text-white bg-emerald-500 px-3 py-1 rounded-full" : "text-xs font-bold text-slate-500 bg-slate-200 px-3 py-1 rounded-full";

            } catch(e) {
                countEl.innerText = "Error";
                countEl.className = "text-xs font-bold text-white bg-red-500 px-3 py-1 rounded-full";
            }
        };

        [input, flags, text].forEach(el => el.addEventListener('input', run));
        run();
    }

    // --- UTILS ---
    function initTabs() {
        const buttons = document.querySelectorAll('.tab-btn');
        const contents = document.querySelectorAll('.tool-content');

        buttons.forEach(btn => {
            btn.addEventListener('click', () => {
                buttons.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                
                contents.forEach(c => c.classList.add('hidden'));
                document.getElementById(btn.dataset.target).classList.remove('hidden');

                // Trigger Monaco Relayout
                if(btn.dataset.target === 'markdown') mdEditor.layout();
                if(btn.dataset.target === 'formatter') { fmtInput.layout(); fmtOutput.layout(); }
                if(btn.dataset.target === 'diff-checker') diffEditor.layout();
            });
        });
    }

    function escapeHtml(text) {
        return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    }

    function downloadFile(filename, content, type) {
        const blob = new Blob([content], { type });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = filename;
        a.click();
        URL.revokeObjectURL(url);
    }
</script>
</body>
</html>
