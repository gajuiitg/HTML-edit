<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mega HTML Editor - 5000 Pages</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #121212;
      color: #e0e0e0;
      height: 100vh;
      overflow: hidden;
    }

    /* ===== TOP FILE BAR (Create / Open / Save) ===== */
    .file-bar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #1e1e2f;
      padding: 10px 20px;
      border-bottom: 2px solid #2d2d44;
      gap: 12px;
      flex-wrap: wrap;
    }
    .file-bar-left, .file-bar-right {
      display: flex;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;
    }
    .file-bar h1 {
      font-size: 18px;
      color: #00d4ff;
      margin-right: 15px;
      white-space: nowrap;
    }
    .btn {
      padding: 10px 18px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      transition: all 0.2s ease;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }
    .btn-new { background: #28a745; color: white; }
    .btn-new:hover { background: #218838; transform: translateY(-2px); }
    .btn-open { background: #17a2b8; color: white; }
    .btn-open:hover { background: #138496; transform: translateY(-2px); }
    .btn-save-html { background: #fd7e14; color: white; }
    .btn-save-html:hover { background: #e56b0a; transform: translateY(-2px); }
    .btn-save-txt { background: #6f42c1; color: white; }
    .btn-save-txt:hover { background: #5a32a3; transform: translateY(-2px); }
    .btn-save-doc { background: #dc3545; color: white; }
    .btn-save-doc:hover { background: #c82333; transform: translateY(-2px); }
    input[type="file"] { display: none; }

    /* ===== FORMATTING TOOLBAR ===== */
    .toolbar {
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
      padding: 8px 20px;
      background: #1a1a2e;
      border-bottom: 1px solid #2d2d44;
      align-items: center;
    }
    .tool-group {
      display: flex;
      gap: 4px;
      padding: 0 8px;
      border-right: 1px solid #2d2d44;
      align-items: center;
    }
    .tool-group:last-child { border-right: none; }
    .tool-btn {
      background: #252540;
      color: #e0e0e0;
      border: 1px solid #3a3a55;
      padding: 6px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      min-width: 34px;
      transition: all 0.15s;
    }
    .tool-btn:hover { background: #00d4ff; color: #000; border-color: #00d4ff; }
    .tool-btn.active { background: #00d4ff; color: #000; }
    .tool-select {
      background: #252540;
      color: #e0e0e0;
      border: 1px solid #3a3a55;
      padding: 6px 8px;
      border-radius: 6px;
      font-size: 12px;
      cursor: pointer;
    }
    .color-picker {
      width: 36px;
      height: 30px;
      border: 1px solid #3a3a55;
      border-radius: 6px;
      cursor: pointer;
      background: #252540;
    }

    /* ===== PAGE NAVIGATION BAR ===== */
    .page-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 8px 20px;
      background: #16162a;
      border-bottom: 1px solid #2d2d44;
      flex-wrap: wrap;
      gap: 10px;
    }
    .page-nav {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .page-nav button {
      background: #252540;
      color: #e0e0e0;
      border: 1px solid #3a3a55;
      padding: 6px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
    }
    .page-nav button:hover { background: #00d4ff; color: #000; }
    .page-info {
      font-size: 14px;
      color: #aaa;
      display: flex;
      align-items: center;
      gap: 6px;
      margin: 0 10px;
    }
    .page-info input {
      width: 55px;
      text-align: center;
      background: #1e1e2f;
      color: #fff;
      border: 1px solid #3a3a55;
      border-radius: 5px;
      padding: 4px;
      font-size: 14px;
    }
    .page-ops button {
      background: #e94560;
      color: white;
      border: none;
      padding: 6px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      margin-left: 6px;
    }
    .page-ops button:first-child { background: #0ead69; }
    .page-ops button:hover { opacity: 0.9; transform: translateY(-1px); }

    /* ===== EDITOR AREA ===== */
    .editor-wrapper {
      flex: 1;
      overflow: auto;
      padding: 25px;
      background: #0a0a15;
      display: flex;
      flex-direction: column;
    }
    #editor {
      background: #ffffff;
      color: #222222;
      min-height: 1100px;
      max-width: 816px;
      width: 100%;
      margin: 0 auto;
      padding: 72px;
      box-shadow: 0 4px 30px rgba(0,0,0,0.6);
      font-family: 'Times New Roman', Times, serif;
      font-size: 12pt;
      line-height: 1.6;
      outline: none;
      border-radius: 2px;
    }
    #editor:focus { box-shadow: 0 4px 40px rgba(0, 212, 255, 0.15); }
    #editor p { margin: 0 0 12px 0; }
    #editor h1, #editor h2, #editor h3, #editor h4 { margin: 16px 0 8px 0; color: #111; }
    #editor table { border-collapse: collapse; width: 100%; margin: 12px 0; }
    #editor td, #editor th { border: 1px solid #bbb; padding: 8px; color: #222; }
    #editor img { max-width: 100%; height: auto; }
    #editor a { color: #0066cc; text-decoration: underline; }
    .page-break {
      page-break-after: always;
      border-bottom: 2px dashed #e94560;
      margin: 20px 0;
      text-align: center;
      color: #e94560;
      font-size: 11px;
      padding: 10px;
      background: #fff0f3;
      pointer-events: none;
      user-select: none;
    }

    /* ===== STATUS BAR ===== */
    .status-bar {
      display: flex;
      gap: 30px;
      padding: 8px 20px;
      background: #1e1e2f;
      border-top: 1px solid #2d2d44;
      font-size: 12px;
      color: #888;
      justify-content: center;
    }

    /* Modal */
    .modal-overlay {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.8);
      z-index: 1000;
      justify-content: center;
      align-items: center;
    }
    .modal-box {
      background: #1e1e2f;
      padding: 30px;
      border-radius: 12px;
      border: 1px solid #3a3a55;
      max-width: 500px;
      width: 90%;
      text-align: center;
    }
    .modal-box h2 { color: #00d4ff; margin-bottom: 15px; }
    .modal-box p { color: #aaa; margin-bottom: 20px; line-height: 1.5; }
    .modal-box button { margin-top: 10px; }

    .main-container { display: flex; flex-direction: column; height: 100vh; }
  </style>
</head>
<body>

<div class="main-container">

  <!-- ===== FILE BAR: CREATE / OPEN / SAVE ===== -->
  <div class="file-bar">
    <div class="file-bar-left">
      <h1>📝 Mega Editor</h1>
      <button class="btn btn-new" onclick="newDocument()" title="Create New Document">➕ New</button>
      <button class="btn btn-open" onclick="document.getElementById('fileInput').click()" title="Open HTML, TXT, or DOC file">📂 Open File</button>
      <input type="file" id="fileInput" accept=".html,.htm,.txt,.doc,.docx" onchange="openFile(this)">
    </div>
    <div class="file-bar-right">
      <button class="btn btn-save-html" onclick="saveAs('html')" title="Save as HTML file">💾 Save as HTML</button>
      <button class="btn btn-save-txt" onclick="saveAs('txt')" title="Save as Plain Text">📝 Save as Text</button>
      <button class="btn btn-save-doc" onclick="saveAs('doc')" title="Save as Word Document">📄 Save as Word</button>
    </div>
  </div>

  <!-- ===== FORMATTING TOOLBAR ===== -->
  <div class="toolbar">
    <div class="tool-group">
      <button class="tool-btn" onclick="execCmd('bold')" title="Bold"><b>B</b></button>
      <button class="tool-btn" onclick="execCmd('italic')" title="Italic"><i>I</i></button>
      <button class="tool-btn" onclick="execCmd('underline')" title="Underline"><u>U</u></button>
      <button class="tool-btn" onclick="execCmd('strikeThrough')" title="Strikethrough"><s>S</s></button>
    </div>
    <div class="tool-group">
      <button class="tool-btn" onclick="execCmd('justifyLeft')" title="Left Align">⬅</button>
      <button class="tool-btn" onclick="execCmd('justifyCenter')" title="Center">↔</button>
      <button class="tool-btn" onclick="execCmd('justifyRight')" title="Right Align">➡</button>
      <button class="tool-btn" onclick="execCmd('justifyFull')" title="Justify">⬌</button>
    </div>
    <div class="tool-group">
      <button class="tool-btn" onclick="execCmd('insertUnorderedList')" title="Bullet List">• List</button>
      <button class="tool-btn" onclick="execCmd('insertOrderedList')" title="Numbered List">1. List</button>
      <button class="tool-btn" onclick="execCmd('outdent')" title="Outdent">←|</button>
      <button class="tool-btn" onclick="execCmd('indent')" title="Indent">|→</button>
    </div>
    <div class="tool-group">
      <select class="tool-select" onchange="execCmd('fontName', this.value); this.value=''">
        <option value="">Font Family</option>
        <option value="Arial">Arial</option>
        <option value="Georgia">Georgia</option>
        <option value="Times New Roman">Times New Roman</option>
        <option value="Courier New">Courier New</option>
        <option value="Verdana">Verdana</option>
        <option value="Impact">Impact</option>
        <option value="Comic Sans MS">Comic Sans</option>
      </select>
      <select class="tool-select" onchange="execCmd('fontSize', this.value); this.value=''">
        <option value="">Font Size</option>
        <option value="1">8pt</option>
        <option value="2">10pt</option>
        <option value="3">12pt</option>
        <option value="4">14pt</option>
        <option value="5">18pt</option>
        <option value="6">24pt</option>
        <option value="7">36pt</option>
      </select>
      <input type="color" class="color-picker" onchange="execCmd('foreColor', this.value)" title="Text Color">
      <input type="color" class="color-picker" onchange="execCmd('hiliteColor', this.value)" value="#ffff00" title="Highlight Color">
    </div>
    <div class="tool-group">
      <button class="tool-btn" onclick="execCmd('removeFormat')" title="Clear Formatting">🧹 Clear</button>
      <button class="tool-btn" onclick="execCmd('undo')" title="Undo">↩ Undo</button>
      <button class="tool-btn" onclick="execCmd('redo')" title="Redo">↪ Redo</button>
    </div>
    <div class="tool-group">
      <button class="tool-btn" onclick="insertLink()" title="Insert Link">🔗 Link</button>
      <button class="tool-btn" onclick="insertImage()" title="Insert Image">🖼 Image</button>
      <button class="tool-btn" onclick="insertTable()" title="Insert Table">▦ Table</button>
      <button class="tool-btn" onclick="execCmd('insertHorizontalRule')" title="Horizontal Rule">― Line</button>
      <button class="tool-btn" onclick="insertPageBreak()" title="Insert Page Break" style="background:#e94560;color:#fff;border-color:#e94560;">⤶ Page Break</button>
    </div>
  </div>

  <!-- ===== PAGE NAVIGATION BAR ===== -->
  <div class="page-bar">
    <div class="page-nav">
      <button onclick="firstPage()" title="First Page">⏮ First</button>
      <button onclick="prevPage()" title="Previous Page">◀ Prev</button>
      <span class="page-info">
        Page <input type="number" id="pageInput" value="1" min="1" onchange="goToPage(this.value)"> of <span id="totalPages">1</span>
      </span>
      <button onclick="nextPage()" title="Next Page">Next ▶</button>
      <button onclick="lastPage()" title="Last Page">Last ⏭</button>
    </div>
    <div class="page-ops">
      <button onclick="addPage()" title="Add New Page">+ Add Page</button>
      <button onclick="deletePage()" title="Delete Current Page">− Delete Page</button>
    </div>
  </div>

  <!-- ===== EDITOR ===== -->
  <div class="editor-wrapper">
    <div id="editor" contenteditable="true" spellcheck="false"></div>
  </div>

  <!-- ===== STATUS BAR ===== -->
  <div class="status-bar">
    <span id="wordCount">Words: 0</span>
    <span id="charCount">Characters: 0</span>
    <span id="pageCountDisplay">Pages: 1</span>
    <span id="cursorPos">Ln 1, Col 1</span>
  </div>

</div>

<!-- Modal -->
<div class="modal-overlay" id="modal">
  <div class="modal-box">
    <h2 id="modalTitle">Notice</h2>
    <p id="modalText">Message</p>
    <button class="btn btn-open" onclick="closeModal()">OK</button>
  </div>
</div>

<script>
  // ===== STATE =====
  let pages = ['<p>Welcome to Mega HTML Editor! Start typing here...</p>'];
  let currentPage = 0;
  const editor = document.getElementById('editor');
  const pageInput = document.getElementById('pageInput');
  const totalPagesEl = document.getElementById('totalPages');

  // ===== INITIALIZE =====
  function updateDisplay() {
    editor.innerHTML = pages[currentPage] || '<p></p>';
    pageInput.value = currentPage + 1;
    totalPagesEl.textContent = pages.length;
    document.getElementById('pageCountDisplay').textContent = 'Pages: ' + pages.length;
    updateStats();
  }

  function saveCurrent() {
    pages[currentPage] = editor.innerHTML;
  }

  // ===== CREATE / NEW =====
  function newDocument() {
    if (!confirm('Start a new document? All unsaved changes will be lost.')) return;
    pages = ['<p></p>'];
    currentPage = 0;
    updateDisplay();
    showModal('New Document', 'A fresh blank document has been created. You can now add up to 5000 pages.');
  }

  // ===== FORMATTING =====
  function execCmd(cmd, val = null) {
    document.execCommand(cmd, false, val);
    editor.focus();
    updateStats();
  }

  function insertLink() {
    const url = prompt('Enter URL (e.g., https://example.com):');
    if (url) execCmd('createLink', url);
  }

  function insertImage() {
    const url = prompt('Enter Image URL:');
    if (url) execCmd('insertImage', url);
  }

  function insertTable() {
    const rows = parseInt(prompt('Number of rows:', '3')) || 3;
    const cols = parseInt(prompt('Number of columns:', '3')) || 3;
    let html = '<table style="border-collapse:collapse;width:100%;border:1px solid #bbb;"><tbody>';
    for (let i = 0; i < rows; i++) {
      html += '<tr>';
      for (let j = 0; j < cols; j++) html += '<td style="border:1px solid #bbb;padding:8px;">Cell</td>';
      html += '</tr>';
    }
    html += '</tbody></table><p></p>';
    execCmd('insertHTML', html);
  }

  function insertPageBreak() {
    execCmd('insertHTML', '<div class="page-break">--- PAGE BREAK ---</div><p></p>');
  }

  // ===== PAGE NAVIGATION =====
  function prevPage() {
    if (currentPage > 0) { saveCurrent(); currentPage--; updateDisplay(); }
    else showModal('Navigation', 'You are already on the first page.');
  }

  function nextPage() {
    if (currentPage < pages.length - 1) { saveCurrent(); currentPage++; updateDisplay(); }
    else showModal('Navigation', 'You are on the last page. Click "+ Add Page" to create more.');
  }

  function firstPage() { saveCurrent(); currentPage = 0; updateDisplay(); }
  function lastPage() { saveCurrent(); currentPage = pages.length - 1; updateDisplay(); }

  function goToPage(n) {
    n = parseInt(n);
    if (n >= 1 && n <= pages.length) { saveCurrent(); currentPage = n - 1; updateDisplay(); }
    else { pageInput.value = currentPage + 1; showModal('Invalid Page', 'Please enter a number between 1 and ' + pages.length); }
  }

  function addPage() {
    if (pages.length >= 5000) { showModal('Limit Reached', 'Maximum 5000 pages allowed.'); return; }
    saveCurrent();
    pages.splice(currentPage + 1, 0, '<p></p>');
    currentPage++;
    updateDisplay();
  }

  function deletePage() {
    if (pages.length <= 1) { showModal('Cannot Delete', 'You must keep at least one page.'); return; }
    if (!confirm('Are you sure you want to delete Page ' + (currentPage + 1) + '?')) return;
    pages.splice(currentPage, 1);
    if (currentPage >= pages.length) currentPage = pages.length - 1;
    updateDisplay();
  }

  // ===== OPEN FILE =====
  function openFile(input) {
    const file = input.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = function(e) {
      const content = e.target.result;
      try {
        if (file.name.endsWith('.txt')) {
          const parts = content.split(/\n={10,}\n/);
          pages = parts.length > 1 ? parts.map(p => '<p>' + p.replace(/\n/g, '<br>') + '</p>') : ['<p>' + content.replace(/\n/g, '<br>') + '</p>'];
        } else {
          const parser = new DOMParser();
          const doc = parser.parseFromString(content, 'text/html');
          const body = doc.body;
          const breaks = body.querySelectorAll('.page-break, [style*="page-break"], hr');
          if (breaks.length > 0) {
            pages = [];
            let current = '';
            body.childNodes.forEach(node => {
              if (node.nodeType === 1 && (node.classList?.contains('page-break') || node.style?.pageBreakAfter || node.tagName === 'HR')) {
                pages.push(current || '<p></p>');
                current = '';
              } else {
                current += node.outerHTML || (node.textContent || '');
              }
            });
            if (current) pages.push(current);
            if (pages.length === 0) pages = [body.innerHTML];
          } else {
            pages = [body.innerHTML];
          }
        }
        currentPage = 0;
        updateDisplay();
        showModal('File Opened', '"' + file.name + '" loaded successfully. Total pages: ' + pages.length);
      } catch (err) {
        showModal('Error', 'Could not read file: ' + err.message);
      }
      input.value = '';
    };
    reader.readAsText(file);
  }

  // ===== SAVE FILE =====
  function saveAs(format) {
    saveCurrent();
    let content = '';
    let mime = '';
    let ext = '';
    let filename = 'MyDocument';

    if (format === 'html') {
      let body = '';
      pages.forEach((p, i) => {
        body += p;
        if (i < pages.length - 1) body += '<div style="page-break-after:always;"></div>';
      });
      content = `<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>MyDocument</title>
<style>
body{font-family:'Times New Roman',serif;max-width:816px;margin:40px auto;padding:60px 72px;line-height:1.6;color:#222;background:#fff;}
p{margin:0 0 12px 0;}
h1,h2,h3,h4{color:#111;margin:16px 0 8px 0;}
table{border-collapse:collapse;width:100%;}
td,th{border:1px solid #ccc;padding:8px;}
img{max-width:100%;height:auto;}
a{color:#0066cc;}
</style>
</head>
<body>
${body}
</body>
</html>`;
      mime = 'text/html';
      ext = '.html';
    }
    else if (format === 'txt') {
      const div = document.createElement('div');
      pages.forEach((p, i) => {
        div.innerHTML = p;
        content += div.innerText;
        if (i < pages.length - 1) content += '\n\n========== PAGE BREAK ==========\n\n';
      });
      mime = 'text/plain';
      ext = '.txt';
    }
    else if (format === 'doc') {
      let body = '';
      pages.forEach((p, i) => {
        body += p;
        if (i < pages.length - 1) body += '<div style="page-break-after:always;"></div>';
      });
      content = `<html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:w="urn:schemas-microsoft-com:office:word" xmlns="http://www.w3.org/TR/REC-html40">
<head>
<meta charset="utf-8">
<title>MyDocument</title>
<style>
body{font-family:'Times New Roman',serif;font-size:12pt;line-height:1.6;}
p{margin:0 0 12pt 0;}
</style>
</head>
<body>
${body}
</body>
</html>`;
      mime = 'application/msword';
      ext = '.doc';
    }

    const blob = new Blob([content], { type: mime });
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = filename + ext;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(a.href);

    showModal('Saved!', 'Your document has been saved as ' + ext.toUpperCase() + ' file.');
  }

  // ===== STATS & UTILS =====
  function updateStats() {
    const text = editor.innerText || '';
    const words = text.trim().split(/\s+/).filter(w => w).length;
    document.getElementById('wordCount').textContent = 'Words: ' + words;
    document.getElementById('charCount').textContent = 'Characters: ' + text.length;

    const sel = window.getSelection();
    if (sel.rangeCount > 0) {
      const range = sel.getRangeAt(0);
      const pre = range.startContainer.textContent ? range.startContainer.textContent.substring(0, range.startOffset) : '';
      const lines = pre.split('\n').length;
      const cols = pre.length - pre.lastIndexOf('\n');
      document.getElementById('cursorPos').textContent = 'Ln ' + lines + ', Col ' + (cols < 0 ? 1 : cols);
    }
  }

  function showModal(title, text) {
    document.getElementById('modalTitle').textContent = title;
    document.getElementById('modalText').textContent = text;
    document.getElementById('modal').style.display = 'flex';
  }

  function closeModal() {
    document.getElementById('modal').style.display = 'none';
  }

  // Event listeners
  editor.addEventListener('input', updateStats);
  editor.addEventListener('keyup', updateStats);
  editor.addEventListener('click', updateStats);

  // Keyboard shortcuts
  document.addEventListener('keydown', function(e) {
    if (e.ctrlKey || e.metaKey) {
      if (e.key === 's') { e.preventDefault(); saveAs('html'); }
      if (e.key === 'o') { e.preventDefault(); document.getElementById('fileInput').click(); }
      if (e.key === 'n') { e.preventDefault(); newDocument(); }
    }
  });

  // Start
  updateDisplay();
</script>

</body>
</html>