const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const PORT = process.env.PORT || 3000;

// Serve the complete application from a single endpoint
app.get('/', (req, res) => {
  res.send(`
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CodeShare - All-in-One Code Sharing</title>
    <style>
        :root {
            --primary-color: #4CAF50;
            --primary-hover: #45a049;
            --background: #f5f5f5;
            --card-bg: #ffffff;
            --text-color: #333333;
            --border-color: #dddddd;
            --code-bg: #282c34;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: var(--background);
            color: var(--text-color);
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
        }

        header h1 {
            color: var(--primary-color);
            margin-bottom: 5px;
        }

        .upload-form {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
        }

        .upload-form h2 {
            margin-top: 0;
            color: var(--primary-color);
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
        }

        input[type="text"],
        select,
        textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            font-family: 'Consolas', 'Monaco', monospace;
        }

        textarea {
            min-height: 200px;
            resize: vertical;
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        .code-list h2 {
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
        }

        .code-snippet {
            background: var(--card-bg);
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            overflow: hidden;
        }

        .snippet-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 15px;
            background-color: var(--primary-color);
            color: white;
        }

        .snippet-title {
            margin: 0;
            font-size: 18px;
        }

        .snippet-language {
            background: rgba(255, 255, 255, 0.2);
            padding: 3px 8px;
            border-radius: 20px;
            font-size: 14px;
        }

        .code-container {
            position: relative;
        }

        .copy-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
            z-index: 10;
        }

        .copy-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        pre {
            margin: 0;
            padding: 15px;
            background: var(--code-bg);
            overflow-x: auto;
        }

        code {
            font-family: 'Consolas', 'Monaco', monospace;
            font-size: 14px;
            color: #abb2bf;
        }

        .loading {
            text-align: center;
            padding: 20px;
            color: #666;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .upload-form {
                padding: 15px;
            }
        }

        /* Simple syntax highlighting */
        .token.comment,
        .token.prolog,
        .token.doctype,
        .token.cdata {
            color: #5c6370;
            font-style: italic;
        }
        .token.punctuation {
            color: #abb2bf;
        }
        .token.selector,
        .token.tag {
            color: #e06c75;
        }
        .token.property,
        .token.boolean,
        .token.number,
        .token.constant,
        .token.symbol,
        .token.attr-name,
        .token.deleted {
            color: #d19a66;
        }
        .token.string,
        .token.char,
        .token.attr-value,
        .token.builtin,
        .token.inserted {
            color: #98c379;
        }
        .token.operator,
        .token.entity,
        .token.url,
        .language-css .token.string,
        .style .token.string {
            color: #56b6c2;
        }
        .token.atrule,
        .token.keyword {
            color: #c678dd;
        }
        .token.function,
        .token.class-name {
            color: #61afef;
        }
        .token.regex,
        .token.important,
        .token.variable {
            color: #c678dd;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>CodeShare</h1>
            <p>Share and copy code snippets with ease</p>
        </header>
        
        <div class="upload-form">
            <h2>Upload Your Code</h2>
            <form id="codeForm">
                <div class="form-group">
                    <label for="title">Title:</label>
                    <input type="text" id="title" placeholder="Give your snippet a name">
                </div>
                <div class="form-group">
                    <label for="language">Language:</label>
                    <select id="language">
                        <option value="javascript">JavaScript</option>
                        <option value="python">Python</option>
                        <option value="html">HTML</option>
                        <option value="css">CSS</option>
                        <option value="java">Java</option>
                        <option value="cpp">C++</option>
                        <option value="php">PHP</option>
                        <option value="ruby">Ruby</option>
                        <option value="plaintext">Plain Text</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="codeInput">Code:</label>
                    <textarea id="codeInput" placeholder="Paste your code here..." spellcheck="false"></textarea>
                </div>
                <button type="submit">Upload Code</button>
            </form>
        </div>
        
        <div class="code-list" id="codeDisplay">
            <h2>Recent Code Snippets</h2>
            <div id="snippetsContainer"></div>
        </div>
    </div>

    <script>
        // In-memory database for the client side
        let codeSnippets = [];
        
        document.addEventListener('DOMContentLoaded', () => {
            // Load all code snippets when page loads
            loadCodeSnippets();
            
            // Handle form submission
            document.getElementById('codeForm').addEventListener('submit', async (e) => {
                e.preventDefault();
                
                const title = document.getElementById('title').value.trim();
                const language = document.getElementById('language').value;
                const code = document.getElementById('codeInput').value.trim();
                
                if (!code) {
                    alert('Please enter some code');
                    return;
                }
                
                try {
                    const response = await fetch('/api/codes', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify({ 
                            title: title || 'Untitled',
                            code, 
                            language 
                        }),
                    });
                    
                    if (!response.ok) {
                        throw new Error('Failed to upload code');
                    }
                    
                    const newCode = await response.json();
                    addCodeSnippetToDOM(newCode);
                    
                    // Reset form
                    document.getElementById('codeForm').reset();
                } catch (error) {
                    console.error('Error:', error);
                    alert('Failed to upload code. Please try again.');
                }
            });
        });

        async function loadCodeSnippets() {
            const container = document.getElementById('snippetsContainer');
            container.innerHTML = '<div class="loading">Loading code snippets...</div>';
            
            try {
                const response = await fetch('/api/codes');
                if (!response.ok) {
                    throw new Error('Failed to load snippets');
                }
                
                const snippets = await response.json();
                container.innerHTML = '';
                
                if (snippets.length === 0) {
                    container.innerHTML = '<div class="loading">No code snippets yet. Be the first to share!</div>';
                    return;
                }
                
                snippets.forEach(snippet => {
                    addCodeSnippetToDOM(snippet);
                });
            } catch (error) {
                console.error('Error:', error);
                container.innerHTML = '<div class="loading">Failed to load code snippets. Please refresh the page.</div>';
            }
        }

        function addCodeSnippetToDOM(snippet) {
            const container = document.getElementById('snippetsContainer');
            
            const snippetElement = document.createElement('div');
            snippetElement.className = 'code-snippet';
            snippetElement.innerHTML = \`
                <div class="snippet-header">
                    <h3 class="snippet-title">\${escapeHtml(snippet.title)}</h3>
                    <span class="snippet-language">\${escapeHtml(snippet.language)}</span>
                </div>
                <div class="code-container">
                    <button class="copy-btn">Copy</button>
                    <pre><code class="language-\${escapeHtml(snippet.language)}">\${escapeHtml(snippet.code)}</code></pre>
                </div>
            \`;
            
            // Add copy functionality
            const copyBtn = snippetElement.querySelector('.copy-btn');
            copyBtn.addEventListener('click', () => {
                copyToClipboard(snippet.code);
                copyBtn.textContent = 'Copied!';
                setTimeout(() => {
                    copyBtn.textContent = 'Copy';
                }, 2000);
            });
            
            // Simple syntax highlighting
            const codeElement = snippetElement.querySelector('code');
            applySyntaxHighlighting(codeElement, snippet.language);
            
            // Prepend to show newest first
            container.prepend(snippetElement);
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                console.log('Code copied to clipboard');
            }).catch(err => {
                console.error('Failed to copy: ', err);
                // Fallback for older browsers
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
            });
        }

        function escapeHtml(unsafe) {
            return unsafe
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }

        // Simple syntax highlighting function
        function applySyntaxHighlighting(element, language) {
            const text = element.textContent;
            let highlighted = escapeHtml(text);
            
            if (language === 'javascript') {
                highlighted = highlighted
                    .replace(/(\bfunction\b|\breturn\b|\bconst\b|\blet\b|\bvar\b|\bif\b|\belse\b|\bfor\b|\bwhile\b|\bdo\b|\btry\b|\bcatch\b|\bfinally\b|\bthrow\b|\bnew\b|\bthis\b|\bclass\b|\bextends\b|\bsuper\b|\bimport\b|\bexport\b|\bdefault\b|\bas\b|\bfrom\b|\basync\b|\bawait\b|\byield\b|\btypeof\b|\binstanceof\b|\bvoid\b|\bdelete\b|\bin\b|\bof\b|\btrue\b|\bfalse\b|\bnull\b|\bundefined\b|\bNaN\b|\bInfinity\b)(?=[^a-zA-Z0-9_])/g, '<span class="token keyword">$1</span>')
                    .replace(/(\/\/.*|\/\*[\s\S]*?\*\/)/g, '<span class="token comment">$1</span>')
                    .replace(/("([^"\\]|\\.)*"|'([^'\\]|\\.)*')/g, '<span class="token string">$1</span>')
                    .replace(/\b(\d+\.?\d*)\b/g, '<span class="token number">$1</span>');
            }
            
            element.innerHTML = highlighted;
        }
    </script>
</body>
</html>
  `);
});

// API backend
app.use(bodyParser.json());

let codes = [];

app.post('/api/codes', (req, res) => {
    const { code, language, title } = req.body;
    if (!code || !language) {
        return res.status(400).json({ error: 'Code and language are required' });
    }
    
    const newCode = {
        id: Date.now().toString(),
        title: title || 'Untitled',
        code,
        language,
        createdAt: new Date().toISOString()
    };
    
    codes.unshift(newCode);
    res.status(201).json(newCode);
});

app.get('/api/codes', (req, res) => {
    res.json(codes);
});

app.get('/api/codes/:id', (req, res) => {
    const code = codes.find(c => c.id === req.params.id);
    if (!code) {
        return res.status(404).json({ error: 'Code not found' });
    }
    res.json(code);
});

app.delete('/api/codes/:id', (req, res) => {
    const index = codes.findIndex(c => c.id === req.params.id);
    if (index === -1) {
        return res.status(404).json({ error: 'Code not found' });
    }
    codes.splice(index, 1);
    res.status(204).end();
});

// Start server
app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
