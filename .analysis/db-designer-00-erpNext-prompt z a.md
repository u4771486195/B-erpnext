Role and Goal: You are an Expert Software Architect and Data Visualization Specialist. Your primary goal is to synthesize multiple partial architectural diagrams—along with their embedded architectural insights—into a single, definitive, and hyper-accurate master visualization of the entire OpenRA game engine.
Context: I will provide you with the full content of separate HTML files. Each file contains a schemaR3 JavaScript object within its <script> tag, representing a fragment of the OpenRA architecture. Crucially, each file also contains a detailed JavaScript comment block beginning with /* ARCHITECTURAL INSIGHTS FOR FUTURE AI ANALYSIS: ... */. Your mission is to merge all these fragments and insights into one cohesive and comprehensive whole.
Core Task: Merge, Synthesize, and Re-render
Your task is to ingest all provided HTML files, extract their schemaR3 data and architectural comments, and merge them into a single, massive, and hyper-accurate HTML visualization. The final output must be a single HTML file containing the complete, deduplicated, and intelligently re-laid-out architectural graph, preceded by a single, synthesized comment block of all aggregated insights.
Critical Requirements & Constraints (Follow Strictly):
Data Extraction: You must parse each HTML file and extract two key pieces of information from within its <script> tag:
The schemaR3 JavaScript object.
The entire multi-line comment block that starts with /* ARCHITECTURAL INSIGHTS FOR FUTURE AI ANALYSIS:.
Architectural Insight Synthesis (New Requirement):
Gather the content of every architectural insight comment block from every file.
Synthesize these comments into a single, comprehensive, and well-organized multi-line comment.
Deduplicate information. For example, many files will state, "The map.yaml file is the instance document." This should only appear once in the final synthesized comment.
Organize the final comment logically. I recommend a structure like:
Overall Architectural Philosophy (Data-driven, Entity-Component, etc.).
Key File Types and Their Roles (C# Classes, YAML files, Lua Scripts, Binary Assets).
The Data Flow Pipeline (e.g., from mod.yaml to rules to map to live Actor).
This synthesized comment block must be placed at the top of the <script> tag in the final HTML file.
Node (Box) Aggregation and Deduplication:
Iterate through every table (node) in every schemaR3 object from all files.
A node is considered a unique entity based on a composite key of its name AND its path.
If you encounter a node with the same name and path that you have already processed, you must intelligently merge its columns and icon data. The goal is to create the most complete version of that node.
NO UNIQUE NODES ARE TO BE DISCARDED. This is the most important rule.
Relationship Aggregation:
Aggregate ALL relationships from all files into a single master list.
A relationship is only a duplicate if it connects the exact same from.table and from.column to the exact same to.table and to.column with the same type. All unique relationships must be preserved.
Verification and Reporting (Mandatory):
Before you begin merging, you must first process all files to get a baseline count.
You must report the following numbers before providing the final HTML:
The total number of HTML files processed.
The Gross Total Number of Nodes (the sum of all nodes from all files before deduplication).
The Final Number of Unique Nodes after the merging and deduplication process.
The number of duplicate nodes that were identified and merged.
The Final Number of Unique Relationships.
Intelligent Relayout:
Do not simply use the original pos: {x, y} coordinates.
You MUST implement a new, automated layout algorithm for the final, massive graph. The goal is to produce a readable and logically organized diagram.
I recommend a layered/hierarchical graph layout. Group nodes by their nodeType into distinct vertical or horizontal layers (e.g., UI -> Code -> Data/Schema -> Service) to make the data flow intuitive.
Step-by-Step Execution Plan:
Initialization: Create a master dictionary for unique nodes, a master set for unique relationships, and a master set for unique lines of text for the architectural insights. Initialize counters for your verification report.
Processing Loop: For each of the HTML files provided:
a. Extract the schemaR3 object and the architectural insight comment block.
b. Insights: Add each line of the comment block to your master insight set (this will handle deduplication).
c. Nodes: Add the number of nodes in this file's schema to your "Gross Total" counter. For each node, create its unique key (name+path). If the key is new, add it to your master dictionary. If it exists, merge the columns.
d. Relationships: For each relationship, add it to your master relationship set.
Synthesis:
a. Assemble the final, synthesized architectural comment from your master insight set.
b. Perform the final counts for your verification report (Gross Total Nodes, Unique Nodes, etc.).
Layout Calculation: Iterate through your final list of unique nodes and apply your chosen automated layout algorithm to calculate a new pos: {x, y} for each one.
Final HTML Generation: Construct a new, single HTML file using the same template.
a. Inside the <script> tag, first write your synthesized architectural insight comment block.
b. Then, declare the schemaR3 object, populating it with your final, deduplicated, and re-laid-out tables (nodes) and relationships.
Final Output:
a. First, present the Verification Report clearly at the top of your response.
b. Then, provide the complete, final, merged HTML code in a single code block.


C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_1_572391tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/DevOps</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Configuration & DevOps
        { id: 101, name: "pyproject.toml", path: "pyproject.toml", nodeType: "service", pos: { x: 50, y: 50 }, icon: "🐍", columns: [ { name: "pandas" }, { name: "rapidfuzz" }, { name: "holidays" }, { name: "googlemaps" }, { name: "plaid-python" } ] },
        { id: 102, name: "package.json", path: "package.json", nodeType: "service", pos: { x: 50, y: 300 }, icon: "📦", columns: [ { name: "onscan.js" } ] },
        { id: 103, name: ".pre-commit-config.yaml", path: ".pre-commit-config.yaml", nodeType: "service", pos: { x: 50, y: 500 }, icon: "🛡️", columns: [ { name: "ruff" }, { name: "prettier" }, { name: "eslint" } ] },
        { id: 104, name: ".mergify.yml", path: ".mergify.yml", nodeType: "service", pos: { x: 50, y: 750 }, icon: "🔄", columns: [ { name: "pull_request_rules" }, { name: "Automatic merge" }, { name: "backport" } ] },
        { id: 105, name: "license.txt", path: "license.txt", nodeType: "service", pos: { x: 50, y: 1000 }, icon: "📄", columns: [ { name: "GNU GENERAL PUBLIC LICENSE" } ] },

        // Backend & Core Logic
        { id: 201, name: "SalesInvoice", path: "erpnext/accounts/doctype/sales_invoice/sales_invoice.py", nodeType: "code", pos: { x: 850, y: 150 }, icon: "🧾", columns: [ { name: "class SalesInvoice(SellingController)" }, { name: "validate()" }, { name: "on_submit()" }, { name: "on_cancel()" }, { name: "get_gl_entries()" } ] },
        { id: 202, name: "POSInvoice", path: "erpnext/accounts/doctype/pos_invoice/pos_invoice.py", nodeType: "code", pos: { x: 450, y: 550 }, icon: "🛒", columns: [ { name: "class POSInvoice(SalesInvoice)" }, { name: "validate()" }, { name: "set_pos_fields()" }, { name: "make_sales_return()" } ] },
        { id: 203, name: "general_ledger.py", path: "erpnext/accounts/general_ledger.py", nodeType: "code", pos: { x: 1250, y: 350 }, icon: "📚", columns: [ { name: "make_gl_entries()" }, { name: "make_reverse_gl_entries()" } ] },
        { id: 204, name: "party.py", path: "erpnext/accounts/party.py", nodeType: "code", pos: { x: 850, y: 850 }, icon: "👥", columns: [ { name: "get_party_details()" }, { name: "get_party_account()" }, { name: "get_due_date()" } ] },
        { id: 205, name: "accounts_utils.py", path: "erpnext/accounts/utils.py", nodeType: "code", pos: { x: 1250, y: 800 }, icon: "🛠️", columns: [ { name: "get_fiscal_year()" }, { name: "get_balance_on()" }, { name: "create_payment_ledger_entry()" } ] },
        { id: 206, name: "PricingRule", path: "erpnext/accounts/doctype/pricing_rule/pricing_rule.py", nodeType: "code", pos: { x: 450, y: 1200 }, icon: "💲", columns: [ { name: "validate()" }, { name: "apply_pricing_rule()" } ] },
        { id: 207, name: "Subscription", path: "erpnext/accounts/doctype/subscription/subscription.py", nodeType: "code", pos: { x: 850, y: 1300 }, icon: "🔄", columns: [ { name: "process()" }, { name: "generate_invoice()" }, { name: "cancel_subscription()" } ] },
        { id: 208, name: "book_appointment.py", path: "erpnext/www/book_appointment/index.py", nodeType: "code", pos: { x: 1250, y: 1500 }, icon: "📅", columns: [ { name: "get_appointment_slots()" }, { name: "create_appointment()" } ] },
        { id: 209, name: "hooks.py", path: "erpnext/hooks.py", nodeType: "code", pos: { x: 450, y: 200 }, icon: "🪝", columns: [ { name: "app_name = 'erpnext'" }, { name: "app_include_js" }, { name: "doc_events" }, { name: "scheduler_events" } ] },
        
        // Frontend & UI / Data Schema
        { id: 301, name: "Sales Invoice Schema", path: "sales_invoice/sales_invoice.json", nodeType: "db", pos: { x: 1650, y: 150 }, icon: "📝", columns: [ { name: "customer", type: "Link" }, { name: "items", type: "Table" }, { name: "taxes", type: "Table" } ] },
        { id: 302, name: "POS Invoice Schema", path: "pos_invoice/pos_invoice.json", nodeType: "db", pos: { x: 1650, y: 550 }, icon: "📝", columns: [ { name: "customer", type: "Link" }, { name: "pos_profile", type: "Link" }, { name: "items", type: "Table" } ] },
        { id: 303, name: "Sales Invoice UI", path: "sales_invoice/sales_invoice.js", nodeType: "ui", pos: { x: 2000, y: 150 }, icon: "💻", columns: [ { name: "refresh()" }, { name: "customer()" }, { name: "make_payment_entry()" } ] },
        { id: 304, name: "POS Invoice UI", path: "pos_invoice/pos_invoice.js", nodeType: "ui", pos: { x: 2000, y: 550 }, icon: "💻", columns: [ { name: "onload()" }, { name: "set_pos_data()" }, { name: "make_sales_return()" } ] },
        { id: 305, name: "Book Appointment Page", path: "book_appointment/index.html", nodeType: "ui", pos: { x: 1650, y: 950 }, icon: "🌐", columns: [ { name: "{% block page_content %}" } ] },
        { id: 306, name: "Book Appointment Logic", path: "book_appointment/index.js", nodeType: "ui", pos: { x: 2000, y: 950 }, icon: "💻", columns: [ { name: "initialise_select_date()" }, { name: "submit()" } ] }
    ],
    relationships: [
        { from: { table: "pyproject.toml" }, to: { table: "hooks.py" }, type: "flow" },
        { from: { table: ".pre-commit-config.yaml" }, to: { table: "pyproject.toml" }, type: "read" },
        { from: { table: "hooks.py", column: "doc_events" }, to: { table: "SalesInvoice" }, type: "flow" },
        { from: { table: "hooks.py", column: "app_include_js" }, to: { table: "Sales Invoice UI" }, type: "flow" },
        { from: { table: "POSInvoice" }, to: { table: "SalesInvoice" }, type: "flow" },
        { from: { table: "SalesInvoice", column: "get_gl_entries()" }, to: { table: "general_ledger.py", column: "make_gl_entries()" } },
        { from: { table: "SalesInvoice", column: "on_cancel()" }, to: { table: "general_ledger.py", column: "make_reverse_gl_entries()" } },
        { from: { table: "SalesInvoice", column: "validate()" }, to: { table: "party.py", column: "get_party_details()" } },
        { from: { table: "SalesInvoice", column: "validate()" }, to: { table: "accounts_utils.py", column: "get_balance_on()" } },
        { from: { table: "POSInvoice", column: "set_pos_fields()" }, to: { table: "party.py", column: "get_party_details()" } },
        { from: { table: "general_ledger.py", column: "make_gl_entries()" }, to: { table: "accounts_utils.py", column: "create_payment_ledger_entry()" } },
        { from: { table: "SalesInvoice", column: "validate()" }, to: { table: "PricingRule", column: "apply_pricing_rule()" } },
        { from: { table: "Subscription", column: "generate_invoice()" }, to: { table: "SalesInvoice" } },
        { from: { table: "Sales Invoice UI" }, to: { table: "Sales Invoice Schema" }, type: "read" },
        { from: { table: "POS Invoice UI" }, to: { table: "POS Invoice Schema" }, type: "read" },
        { from: { table: "Sales Invoice UI", column: "customer()" }, to: { table: "party.py", column: "get_party_details()" } },
        { from: { table: "POS Invoice UI", column: "set_pos_data()" }, to: { table: "POSInvoice", column: "set_missing_values()" } },
        { from: { table: "Book Appointment Logic", column: "submit()" }, to: { table: "book_appointment.py", column: "create_appointment()" } },
        { from: { table: "Book Appointment Logic", column: "update_time_slots()" }, to: { table: "book_appointment.py", column: "get_appointment_slots()" } },
        { from: { table: "Book Appointment Page" }, to: { table: "Book Appointment Logic" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_2_578578tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 2</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 2
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Bank Statement Import
        { id: 401, name: "Bank Statement Import UI", path: "accounts/doctype/bank_statement_import/bank_statement_import.js", nodeType: "ui", pos: { x: 50, y: 50 }, icon: " Mapextract", columns: [ { name: "start_import()" }, { name: "convert_mt940_to_csv()" } ] },
        { id: 402, name: "Bank Statement Import Logic", path: "accounts/doctype/bank_statement_import/bank_statement_import.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: " Mapextract", columns: [ { name: "class BankStatementImport(DataImport)" }, { name: "start_import() -> enqueue" }, { name: "convert_mt940_to_csv()" }, { name: "start_import() -> (background job)" } ] },
        { id: 403, name: "Bank Statement Import Schema", path: "accounts/doctype/bank_statement_import/bank_statement_import.json", nodeType: "db", pos: { x: 850, y: 50 }, icon: "📝", columns: [ { name: "import_file", type: "Attach" }, { name: "bank_account", type: "Link" }, { name: "status", type: "Select" } ] },
        { id: 404, name: "MT940 Library", path: "(external library)", nodeType: "service", pos: { x: 850, y: 300 }, icon: "📦", columns: [ { name: "mt940.parse()" } ] },
        { id: 405, name: "Bank Transaction Schema", path: "accounts/doctype/bank_transaction/bank_transaction.json", nodeType: "db", pos: { x: 1250, y: 50 }, icon: "🏦", columns: [ { name: "date", type: "Date" }, { name: "deposit", type: "Currency" }, { name: "withdrawal", type: "Currency" } ] },

        // Payment Request & Subscriptions
        { id: 406, name: "Payment Request UI", path: "accounts/doctype/payment_request/payment_request.js", nodeType: "ui", pos: { x: 50, y: 500 }, icon: "💳", columns: [ { name: "Create Payment Entry" }, { name: "is_a_subscription" } ] },
        { id: 407, name: "Payment Request Logic", path: "accounts/doctype/payment_request/payment_request.py", nodeType: "code", pos: { x: 450, y: 500 }, icon: "💳", columns: [ { name: "set_as_paid() -> create_payment_entry()" }, { name: "get_payment_url()" }, { name: "create_subscription()" } ] },
        { id: 408, name: "Payment Request Schema", path: "accounts/doctype/payment_request/payment_request.json", nodeType: "db", pos: { x: 850, y: 500 }, icon: "📝", columns: [ { name: "is_a_subscription", type: "Check" }, { name: "subscription_plans", type: "Table" }, { name: "status", type: "Select" } ] },
        { id: 409, name: "Payment Entry Schema", path: "accounts/doctype/payment_entry/payment_entry.json", nodeType: "db", pos: { x: 1250, y: 650 }, icon: "💵", columns: [ { name: "payment_type", type: "Select" }, { name: "party", type: "Dynamic Link" }, { name: "paid_amount", type: "Currency" } ] },
        { id: 417, name: "Subscription Plan Schema", path: "accounts/doctype/subscription_plan/subscription_plan.json", nodeType: "db", pos: { x: 850, y: 800 }, icon: "🔄", columns: [ { name: "plan_name", type: "Data" }, { name: "cost", type: "Currency" }, { name: "billing_interval", type: "Select" } ] },
        
        // POS Closing & Invoice Consolidation
        { id: 410, name: "POS Closing Entry Logic", path: "accounts/doctype/pos_closing_entry/pos_closing_entry.py", nodeType: "code", pos: { x: 50, y: 1000 }, icon: "🧾", columns: [ { name: "on_submit() -> consolidate_pos_invoices()" } ] },
        { id: 411, name: "POS Invoice Merge Log Logic", path: "accounts/doctype/pos_invoice_merge_log/pos_invoice_merge_log.py", nodeType: "code", pos: { x: 450, y: 1000 }, icon: "🧾", columns: [ { name: "consolidate_pos_invoices()" }, { name: "on_submit() -> process_merging_into_sales_invoice()" } ] },
        { id: 201, name: "SalesInvoice", path: "erpnext/accounts/doctype/sales_invoice/sales_invoice.py", nodeType: "code", pos: { x: 850, y: 1000 }, icon: "🧾", columns: [ { name: "class SalesInvoice(...)" }, { name: "on_submit()" } ] },

        // Purchase Invoice
        { id: 412, name: "Purchase Invoice UI", path: "accounts/doctype/purchase_invoice/purchase_invoice.js", nodeType: "ui", pos: { x: 50, y: 1250 }, icon: "🛒", columns: [ { name: "Get Items From -> Purchase Order" }, { name: "Get Items From -> Purchase Receipt" } ] },
        { id: 413, name: "Purchase Invoice Logic", path: "accounts/doctype/purchase_invoice/purchase_invoice.py", nodeType: "code", pos: { x: 450, y: 1250 }, icon: "🛒", columns: [ { name: "on_submit()" }, { name: "make_gl_entries()" }, { name: "update_stock_ledger()" } ] },
        { id: 414, name: "Purchase Invoice Schema", path: "accounts/doctype/purchase_invoice/purchase_invoice.json", nodeType: "db", pos: { x: 850, y: 1250 }, icon: "📝", columns: [ { name: "supplier", type: "Link" }, { name: "items", type: "Table" }, { name: "update_stock", type: "Check" } ] },
        { id: 415, name: "General Ledger Process", path: "(Core Process)", nodeType: "code", pos: { x: 1250, y: 1150 }, icon: "📚", columns: [ { name: "make_gl_entries()" } ] },
        { id: 416, name: "Stock Ledger Process", path: "(Core Process)", nodeType: "code", pos: { x: 1250, y: 1350 }, icon: "📦", columns: [ { name: "update_stock_ledger()" } ] }
    ],
    relationships: [
        // Bank Statement Import
        { from: { table: "Bank Statement Import UI", column: "convert_mt940_to_csv()" }, to: { table: "Bank Statement Import Logic", column: "convert_mt940_to_csv()" } },
        { from: { table: "Bank Statement Import UI" }, to: { table: "Bank Statement Import Schema" }, type: "read" },
        { from: { table: "Bank Statement Import Logic", column: "class BankStatementImport(DataImport)" }, to: { table: "MT940 Library", column: "mt940.parse()" }, type: "flow" },
        { from: { table: "Bank Statement Import Logic", column: "start_import() -> (background job)" }, to: { table: "Bank Transaction Schema" }, type: "write" },
        
        // Payment Request & Subscriptions
        { from: { table: "Payment Request UI", column: "Create Payment Entry" }, to: { table: "Payment Request Logic", column: "set_as_paid() -> create_payment_entry()" } },
        { from: { table: "Payment Request Logic", column: "set_as_paid() -> create_payment_entry()" }, to: { table: "Payment Entry Schema" }, type: "write" },
        { from: { table: "Payment Request UI", column: "is_a_subscription" }, to: { table: "Payment Request Schema", column: "is_a_subscription" } },
        { from: { table: "Payment Request Schema", column: "subscription_plans" }, to: { table: "Subscription Plan Schema" }, type: "read" },
        { from: { table: "Payment Request Logic", column: "create_subscription()" }, to: { table: "Subscription Plan Schema" }, type: "flow" },
        
        // POS Closing
        { from: { table: "POS Closing Entry Logic", column: "on_submit() -> consolidate_pos_invoices()" }, to: { table: "POS Invoice Merge Log Logic", column: "consolidate_pos_invoices()" } },
        { from: { table: "POS Invoice Merge Log Logic", column: "on_submit() -> process_merging_into_sales_invoice()" }, to: { table: "SalesInvoice" }, type: "write" },

        // Purchase Invoice
        { from: { table: "Purchase Invoice Logic", column: "make_gl_entries()" }, to: { table: "General Ledger Process", column: "make_gl_entries()" } },
        { from: { table: "Purchase Invoice Logic", column: "update_stock_ledger()" }, to: { table: "Stock Ledger Process", column: "update_stock_ledger()" } },
        { from: { table: "Purchase Invoice UI" }, to: { table: "Purchase Invoice Logic" }, type: "read" },
        { from: { table: "Purchase Invoice Logic" }, to: { table: "Purchase Invoice Schema" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_4_473604tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 3</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 3
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Payment Entry Core
        { id: 501, name: "Payment Entry Logic", path: "accounts/doctype/payment_entry/payment_entry.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "⚙️", columns: [ { name: "on_submit()" }, { name: "make_gl_entries()" }, { name: "validate_reference_documents()" }, { name: "set_amounts()" }, { name: "clear_unallocated_reference_document_rows()" }, { name: "build_gl_map()" } ] },
        { id: 502, name: "Payment Entry Schema", path: "accounts/doctype/payment_entry/payment_entry.json", nodeType: "db", pos: { x: 850, y: 50 }, icon: "📝", columns: [ { name: "party_type" }, { name: "payment_type" }, { name: "references", type: "Table" }, { name: "deductions", type: "Table" } ] },
        { id: 503, name: "Payment Entry UI", path: "accounts/doctype/payment_entry/payment_entry_list.js", nodeType: "ui", pos: { x: 50, y: 50 }, icon: "💻", columns: [ { name: "onload()" }, { name: "allocate_amount_to_references()" }, { name: "get_outstanding_reference_documents()" } ] },
        { id: 504, name: "General Ledger Process", path: "accounts/general_ledger.py", nodeType: "code", pos: { x: 850, y: 400 }, icon: "📚", columns: [ { name: "make_gl_entries()" }, { name: "process_gl_map()" } ] },
        { id: 505, name: "Payment Ledger Update", path: "(Core Process)", nodeType: "code", pos: { x: 850, y: 600 }, icon: " ledger", columns: [ { name: "update_payment_schedule()" }, { name: "update_outstanding_on_submit()" } ] },

        // Bank Reconciliation
        { id: 506, name: "Bank Reconciliation UI", path: "accounts/doctype/bank_reconciliation_tool/bank_reconciliation_tool.js", nodeType: "ui", pos: { x: 50, y: 900 }, icon: "🏦", columns: [ { name: "make_reconciliation_tool()" }, { name: "Auto Reconcile" }, { name: "Get Unreconciled Entries" } ] },
        { id: 507, name: "Bank Reconciliation Logic", path: "accounts/doctype/bank_reconciliation_tool/bank_reconciliation_tool.py", nodeType: "code", pos: { x: 450, y: 900 }, icon: "🧠", columns: [ { name: "get_bank_transactions()" }, { name: "auto_reconcile_vouchers()" }, { name: "reconcile_vouchers()" }, { name: "create_journal_entry_bts()" }, { name: "create_payment_entry_bts()" } ] },
        { id: 508, name: "Bank Transaction Schema", path: "accounts/doctype/bank_transaction/bank_transaction.json", nodeType: "db", pos: { x: 850, y: 900 }, icon: "🧾", columns: [ { name: "date" }, { name: "deposit" }, { name: "withdrawal" }, { name: "unallocated_amount" } ] },

        // Account & CoA
        { id: 509, name: "Account Logic", path: "accounts/doctype/account/account.py", nodeType: "code", pos: { x: 450, y: 1300 }, icon: "🏛️", columns: [ { name: "validate()" }, { name: "merge_account()" }, { name: "update_account_number()" }, { name: "create_account_for_child_company()" } ] },
        { id: 510, name: "Account Schema", path: "accounts/doctype/account/account.json", nodeType: "db", pos: { x: 850, y: 1300 }, icon: "📝", columns: [ { name: "account_name" }, { name: "is_group" }, { name: "parent_account" }, { name: "company" }, { name: "root_type" } ] },
        { id: 511, name: "Chart of Accounts Tree", path: "accounts/doctype/account/account_tree.js", nodeType: "ui", pos: { x: 50, y: 1300 }, icon: "🌲", columns: [ { name: "get_tree_nodes()" }, { name: "add_tree_node()" }, { name: "get_account_balances()" } ] },
        { id: 512, name: "CoA Template (AU)", path: "chart_of_accounts/verified/au_standard_chart_of_accounts.json", nodeType: "service", pos: { x: 850, y: 1550 }, icon: "📄", columns: [ { name: "Assets" }, { name: "Liabilities" }, { name: "Equity" } ] },
        { id: 513, name: "CoA Template Importer", path: "chart_of_accounts/chart_of_accounts.py", nodeType: "code", pos: { x: 450, y: 1550 }, icon: "📥", columns: [ { name: "create_charts()" }, { name: "get_charts_for_country()" }, { name: "build_tree_from_json()" } ] },

        // Dunning
        { id: 514, name: "Dunning Type Schema", path: "accounts/doctype/dunning_type/dunning_type.json", nodeType: "db", pos: { x: 450, y: 1800 }, icon: "📝", columns: [ { name: "dunning_fee" }, { name: "rate_of_interest" }, { name: "income_account" } ] },
        { id: 515, name: "Dunning Process", path: "(Implied)", nodeType: "code", pos: { x: 50, y: 1800 }, icon: "🔔", columns: [ { name: "Create Dunning Letter" }, { name: "Calls -> get_payment_entry()" } ] },
        
        // Tests
        { id: 516, name: "Payment Entry Tests", path: "accounts/doctype/payment_entry/test_payment_entry.py", nodeType: "service", pos: { x: 1250, y: 50 }, icon: "🧪", columns: [ { name: "test_payment_entry_against_order()" }, { name: "test_payment_entry_against_si_usd_to_inr()" }, { name: "test_payment_entry_against_payment_terms()" }, { name: "test_reverse_payment_reconciliation()" } ] },

        // Other Child Tables/Doctypes
        { id: 517, name: "POS Invoice Item Schema", path: "accounts/doctype/pos_invoice_item/pos_invoice_item.json", nodeType: "db", pos: { x: 1250, y: 500 }, icon: "🛒", columns: [ { name: "item_code" }, { name: "qty" }, { name: "rate" } ] },
        { id: 518, name: "Accounting Dimension Detail Schema", path: "accounts/doctype/accounting_dimension_detail.json", nodeType: "db", pos: { x: 1250, y: 700 }, icon: "🔗", columns: [ { name: "company" }, { name: "default_dimension" } ] },
        { id: 519, name: "Mode of Payment Account Schema", path: "accounts/doctype/mode_of_payment_account.json", nodeType: "db", pos: { x: 1250, y: 900 }, icon: "🔗", columns: [ { name: "company" }, { name: "default_account" } ] }
    ],
    relationships: [
        // Payment Entry Flow
        { from: { table: "Payment Entry UI" }, to: { table: "Payment Entry Logic" }, type: "flow" },
        { from: { table: "Payment Entry Logic", column: "make_gl_entries()" }, to: { table: "General Ledger Process" }, type: "write" },
        { from: { table: "Payment Entry Logic", column: "on_submit()" }, to: { table: "Payment Ledger Update" }, type: "write" },
        { from: { table: "Payment Entry Logic" }, to: { table: "Payment Entry Schema" }, type: "read" },
        { from: { table: "Payment Entry Tests" }, to: { table: "Payment Entry Logic" }, type: "flow" },

        // Bank Reconciliation Flow
        { from: { table: "Bank Reconciliation UI" }, to: { table: "Bank Reconciliation Logic" }, type: "flow" },
        { from: { table: "Bank Reconciliation Logic", column: "get_bank_transactions()" }, to: { table: "Bank Transaction Schema" }, type: "read" },
        { from: { table: "Bank Reconciliation Logic", column: "reconcile_vouchers()" }, to: { table: "Bank Transaction Schema" }, type: "write" },
        { from: { table: "Bank Reconciliation Logic", column: "create_payment_entry_bts()" }, to: { table: "Payment Entry Logic" }, type: "write" },
        { from: { table: "Bank Reconciliation Logic", column: "create_journal_entry_bts()" }, to: { table: "General Ledger Process" }, type: "write" },
        
        // Chart of Accounts Flow
        { from: { table: "Chart of Accounts Tree" }, to: { table: "Account Logic" }, type: "flow" },
        { from: { table: "Account Logic" }, to: { table: "Account Schema" }, type: "write" },
        { from: { table: "CoA Template Importer", column: "create_charts()" }, to: { table: "Account Logic" }, type: "write" },
        { from: { table: "CoA Template Importer", column: "get_charts_for_country()" }, to: { table: "CoA Template (AU)" }, type: "read" },
        { from: { table: "CoA Template Importer", column: "build_tree_from_json()" }, to: { table: "CoA Template (AU)" }, type: "read" },

        // Dunning Flow
        { from: { table: "Dunning Process" }, to: { table: "Dunning Type Schema" }, type: "read" },
        { from: { table: "Dunning Process", column: "Calls -> get_payment_entry()" }, to: { table: "Payment Entry Logic" }, type: "flow" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_6_499825tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 4</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 4: Chart of Accounts
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        { id: 601, name: "Germany - SKR 03", path: "verified/de_skr03.json", nodeType: "db", pos: { x: 50, y: 50 }, icon: "🇩🇪", columns: [ { name: "ANLAGE- UND KAPITALVERMÖGEN" }, { name: "UMLAUFVERMÖGEN" }, { name: "ERTRÄGE" } ] },
        { id: 602, name: "Algeria - Plan Comptable", path: "verified/dz_plan_comptable_general_avec_code.json", nodeType: "db", pos: { x: 350, y: 50 }, icon: "🇩🇿", columns: [ { name: "CLASSE 1 : CAPITAUX" }, { name: "CLASSE 2 : IMMOBILISATIONS" }, { name: "CLASSE 6 : CHARGES" } ] },
        { id: 603, name: "El Salvador - Standard", path: "verified/el_salvador_standard.json", nodeType: "db", pos: { x: 650, y: 50 }, icon: "🇸🇻", columns: [ { name: "ACTIVOS" }, { name: "PASIVOS" }, { name: "PATRIMONIO" } ] },
        { id: 604, name: "France - Associatif", path: "verified/fr_plan_comptable_associatif_avec_code.json", nodeType: "db", pos: { x: 950, y: 50 }, icon: "🇫🇷", columns: [ { name: "Comptes de Capitaux" }, { name: "Comptes de Charges" }, { name: "Comptes de Produits" } ] },
        { id: 605, name: "France - General", path: "verified/fr_plan_comptable_general.json", nodeType: "db", pos: { x: 1250, y: 50 }, icon: "🇫🇷", columns: [ { name: "1-Comptes de Capitaux" }, { name: "6-Comptes de Charges" }, { name: "7-Comptes de Produits" } ] },
        { id: 606, name: "Gabon - Syscohada", path: "verified/ga_plan_comptable.json", nodeType: "db", pos: { x: 50, y: 400 }, icon: "🇬🇦", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 607, name: "Guinea - Syscohada", path: "verified/gn_plan_comptable.json", nodeType: "db", pos: { x: 350, y: 400 }, icon: "🇬🇳", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 608, name: "Equatorial Guinea - Syscohada", path: "verified/gq_plan_comptable.json", nodeType: "db", pos: { x: 650, y: 400 }, icon: "🇬🇶", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 609, name: "Hungary - Standard", path: "verified/hu_chart_of_accounts.json", nodeType: "db", pos: { x: 950, y: 400 }, icon: "🇭🇺", columns: [ { name: "1. BEFEKTETETT ESZKÖZÖK" }, { name: "5. KÖLTSÉGNEMEK" }, { name: "9. BEVÉTELEK" } ] },
        { id: 610, name: "Hungary - Microenterprises", path: "verified/hu_chart_of_accounts_for_microenterprises_with_account_number.json", nodeType: "db", pos: { x: 1250, y: 400 }, icon: "🇭🇺", columns: [ { name: "BEFEKTETETT ESZKÖZÖK" }, { name: "FORRÁSOK" }, { name: "KÖLTSÉGNEMEK" } ] },
        { id: 611, name: "Indonesia - Standard", path: "verified/id_chart_of_accounts.json", nodeType: "db", pos: { x: 50, y: 750 }, icon: "🇮🇩", columns: [ { name: "Aktiva" }, { name: "Passiva" }, { name: "Beban" } ] },
        { id: 612, name: "Comoros - Syscohada", path: "verified/km_plan_comptable.json", nodeType: "db", pos: { x: 350, y: 750 }, icon: "🇰🇲", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 613, name: "Mali - Syscohada", path: "verified/ml_plan_comptable.json", nodeType: "db", pos: { x: 650, y: 750 }, icon: "🇲🇱", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 614, name: "Mexico - Plan de Cuentas", path: "verified/mx_plan_de_cuentas.json", nodeType: "db", pos: { x: 950, y: 750 }, icon: "🇲🇽", columns: [ { name: "ACTIVO" }, { name: "PASIVO" }, { name: "CAPITAL" } ] },
        { id: 615, name: "Niger - Syscohada", path: "verified/ne_plan_comptable.json", nodeType: "db", pos: { x: 1250, y: 750 }, icon: "🇳🇪", columns: [ { name: "1-Comptes de ressources durables" }, { name: "6-Comptes de charges" }, { name: "7-Comptes de produits" } ] },
        { id: 616, name: "Netherlands - Grootboekschema", path: "verified/nl_grootboekschema.json", nodeType: "db", pos: { x: 50, y: 1100 }, icon: "🇳🇱", columns: [ { name: "VASTE ACTIVA" }, { name: "KORTLOPENDE SCHULDEN" }, { name: "FABRIKAGEREKENINGEN" } ] },
        { id: 617, name: "Portugal - Plano de Contas SNC", path: "verified/pt_pt_chart_template.json", nodeType: "db", pos: { x: 350, y: 1100 }, icon: "🇵🇹", columns: [ { name: "1 - Meios financeiros líquidos" }, { name: "5 - Capital, reservas" }, { name: "6 - Gastos" } ] },
        { id: 618, name: "India - Standard", path: "verified/in_standard_chart_of_accounts.json", nodeType: "db", pos: { x: 650, y: 1100 }, icon: "🇮🇳", columns: [ { name: "Application of Funds (Assets)" }, { name: "Source of Funds (Liabilities)" }, { name: "Expenses" } ] }
    ],
    relationships: []
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_7_447039tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 5</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 5: Chart of Accounts (International)
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Standard Templates
        { id: 701, name: "Standard CoA Template", path: "verified/standard_chart_of_accounts.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "🐍", columns: [ { name: "get()" }, { name: "Application of Funds (Assets)" }, { name: "Source of Funds (Liabilities)" } ] },
        { id: 702, name: "Standard CoA (with Numbers)", path: "verified/standard_chart_of_accounts_with_account_number.py", nodeType: "code", pos: { x: 50, y: 350 }, icon: "🐍", columns: [ { name: "get()" }, { name: "1000 - Application of Funds" }, { name: "2000 - Source of Funds" } ] },
        
        // SYSCOHADA Templates & Generator
        { id: 703, name: "Syscohada CoA Generator", path: "verified/syscohada_chart_of_accounts.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "⚙️", columns: [ { name: "syscohada_countries = [...]" }, { name: "Generates charts for 17 countries" } ] },
        { id: 704, name: "Syscohada Generic Template", path: "verified/syscohada_plan_comptable.json", nodeType: "db", pos: { x: 850, y: 50 }, icon: "📄", columns: [ { name: "1-Comptes de ressources durables" }, { name: "2-Comptes d’actif immobilisé" }, { name: "6-Comptes de charges..." } ] },
        { id: 705, name: "Senegal - Syscohada CoA", path: "verified/sn_plan_comptable.json", nodeType: "db", pos: { x: 1250, y: 50 }, icon: "🇸🇳", columns: [ { name: "root_type: Equity" }, { name: "root_type: Asset" } ] },
        { id: 706, name: "Chad - Syscohada CoA", path: "verified/td_plan_comptable.json", nodeType: "db", pos: { x: 1250, y: 350 }, icon: "🇹🇩", columns: [ { name: "root_type: Equity" }, { name: "root_type: Asset" } ] },
        { id: 707, name: "Togo - Syscohada CoA", path: "verified/tg_plan_comptable.json", nodeType: "db", pos: { x: 1250, y: 650 }, icon: "🇹🇬", columns: [ { name: "root_type: Equity" }, { name: "root_type: Asset" } ] },

        // Other Country-Specific Charts
        { id: 708, name: "Sweden - BAS 2024", path: "verified/se_kontoplan_BAS_2024_with_account_number.json", nodeType: "db", pos: { x: 50, y: 650 }, icon: "🇸🇪", columns: [ { name: "1 Tillgångar" }, { name: "2 Eget Kapital och Skulder" }, { name: "3 Rörelsens inkomster/intäkter" } ] },
        { id: 709, name: "Singapore - Default CoA", path: "verified/sg_default_coa.json", nodeType: "db", pos: { x: 450, y: 650 }, icon: "🇸🇬", columns: [ { name: "Assets" }, { name: "Liabilities" }, { name: "Expenses-Operating" } ] },
        { id: 710, name: "Singapore - F&B CoA", path: "verified/sg_fnb_coa.json", nodeType: "db", pos: { x: 450, y: 950 }, icon: "🇸🇬", columns: [ { name: "Assets" }, { name: "Expenses-Operating" }, { name: "COS-Food" }, { name: "COS-Beverage" } ] },
        { id: 711, name: "Turkey - Chart of Accounts", path: "verified/tr_chart_of_accounts.json", nodeType: "db", pos: { x: 850, y: 650 }, icon: "🇹🇷", columns: [ { name: "DÖNEN VARLIKLAR (Current Assets)" }, { name: "DURAN VARLIKLAR (Fixed Assets)" }, { name: "KISA VADELİ YABANCI KAYNAKLAR" } ] }
    ],
    relationships: [
        { from: { table: "Syscohada CoA Generator" }, to: { table: "Syscohada Generic Template" }, type: "read" },
        { from: { table: "Syscohada CoA Generator" }, to: { table: "Senegal - Syscohada CoA" }, type: "write" },
        { from: { table: "Syscohada CoA Generator" }, to: { table: "Chad - Syscohada CoA" }, type: "write" },
        { from: { table: "Syscohada CoA Generator" }, to: { table: "Togo - Syscohada CoA" }, type: "write" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_8_538858tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 6</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 6: Chart of Accounts (International)
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        { id: 801, name: "Turkey - Chart of Accounts", path: "verified/tr_chart_of_accounts.json", nodeType: "db", pos: { x: 50, y: 50 }, icon: "🇹🇷", columns: [ { name: "DÖNEN VARLIKLAR (Current Assets)" }, { name: "NAZIM HESAPLAR" } ] },
        { id: 802, name: "Taiwan - Chart of Accounts", path: "verified/tw_chart_of_accounts.json", nodeType: "db", pos: { x: 350, y: 50 }, icon: "🇹🇼", columns: [ { name: "所得稅費用(利益)" }, { name: "業主權益" }, { name: "營業外收入及費用" }, { name: "營業成本" }, { name: "營業收入" }, { name: "營業費用" }, { name: "負債" }, { name: "資產" }, { name: "非經常營業損益" } ] },
        { id: 803, name: "Austria - Chart of Accounts", path: "unverified/at_austria_chart_template.json", nodeType: "db", pos: { x: 650, y: 50 }, icon: "🇦🇹", columns: [ { name: "Klasse 0 Aktiva: Anlagevermögen" }, { name: "Klasse 1 Aktiva: Vorräte" }, { name: "Klasse 3 Passiva: Verbindlichkeiten" }, { name: "Klasse 2 Aktiva: Umlaufvermögen, Rechnungsabgrenzungen" }, { name: "Klasse 4: Betriebliche Erträge" } ] },
        { id: 804, name: "Belgian - PCMN", path: "unverified/be_l10nbe_chart_template.json", nodeType: "db", pos: { x: 950, y: 50 }, icon: "🇧🇪", columns: [ { name: "CLASSE 1" }, { name: "CLASSE 2. FRAIS D'ETABLISSEMENT..." }, { name: "CLASSE 3. STOCK ET COMMANDES..." }, { name: "CLASSE 4. CREANCES ET DETTES..." }, { name: "CLASSE 5. PLACEMENTS DE TRESORERIE..." }, { name: "CLASSE 6. - CHARGES" }, { name: "CLASSE 7. - PRODUITS" } ] },
        { id: 805, name: "Switzerland - Plan comptable STERCHI", path: "unverified/ch_l10nch_chart_template.json", nodeType: "db", pos: { x: 50, y: 350 }, icon: "🇨🇭", columns: [ { name: "Actif" }, { name: "Passif" }, { name: "Autres charges d'exploitation" }, { name: "Charges de matières, marchandises et services" }, { name: "Charges de personnel" } ] },
        { id: 806, name: "Chile - Plan de Cuentas", path: "unverified/cl_cl_chart_template.json", nodeType: "db", pos: { x: 350, y: 350 }, icon: "🇨🇱", columns: [ { name: "Cuentas de Movimiento" }, { name: "Cuentas de Orden" }, { name: "Cuentas de Resultado" }, { name: "inventario del Balance General" } ] },
        { id: 807, name: "China - Chart of Accounts", path: "unverified/cn_l10n_chart_china.json", nodeType: "db", pos: { x: 650, y: 350 }, icon: "🇨🇳", columns: [ { name: "主营业务成本" }, { name: "主营业务收入" }, { name: "交易性金融负债" }, { name: "交易性金融资产" } ] },
        { id: 808, name: "Costa Rica - Chart of Accounts 1", path: "unverified/cr_account_chart_template_0.json", nodeType: "db", pos: { x: 950, y: 350 }, icon: "🇨🇷", columns: [ { name: "0-Activo" }, { name: "0-Gastos" }, { name: "0-Ingresos" }, { name: "0-Pasivo" }, { name: "0-Patrimonio" } ] },
        { id: 809, name: "Costa Rica - Chart of Accounts 2", path: "unverified/cr_account_chart_template_x.json", nodeType: "db", pos: { x: 50, y: 650 }, icon: "🇨🇷", columns: [ { name: "xActivo" }, { name: "xGastos" }, { name: "xIngresos" }, { name: "xPasivo" }, { name: "xPatrimonio" } ] },
        { id: 810, name: "Germany - Kontenplan SKR03", path: "unverified/de_l10n_de_chart_template.json", nodeType: "db", pos: { x: 350, y: 650 }, icon: "🇩🇪", columns: [ { name: "Aktiva" }, { name: "Passiva" }, { name: "Ergebnis vor Steuern" }, { name: "Steuern Eink.u.Ertr" }, { name: "Vortrags- Kapital- und Statistische Konten" } ] },
        { id: 811, name: "Ecuador - Chart of Accounts", path: "unverified/ec_ec_chart_template.json", nodeType: "db", pos: { x: 650, y: 650 }, icon: "🇪🇨", columns: [ { name: "ACTIVO CORRIENTE" }, { name: "ACTIVOS BIOLOGICOS" }, { name: "ACTIVOS FINANCIEROS" }, { name: "ACTIVOS NO CORRIENTES" } ] },
        { id: 812, name: "Spain - PGCE común", path: "unverified/es_account_chart_template_common.json", nodeType: "db", pos: { x: 950, y: 650 }, icon: "🇪🇸", columns: [ { name: "Acreedores y deudores..." }, { name: "Activo no corriente" }, { name: "Compras y gastos" }, { name: "Cuentas financieras" }, { name: "Existencias" } ] },
        { id: 813, name: "Ethiopia - Chart of Accounts", path: "unverified/et_l10n_et.json", nodeType: "db", pos: { x: 50, y: 950 }, icon: "🇪🇹", columns: [ { name: "ASSETS" }, { name: "COST OF GOODS SOLD" }, { name: "EXPENSES" }, { name: "LIABILITIES" }, { name: "NET ASSETS/EQUITY" }, { name: "REVENUE" } ] },
        { id: 814, name: "Greece - Chart of Accounts", path: "unverified/gr_l10n_gr_chart_template.json", nodeType: "db", pos: { x: 350, y: 950 }, icon: "🇬🇷", columns: [ { name: "ΑΠΑΙΤΗΣΕΙΣ ΚΑΙ ΔΙΑΘΕΣΙΜΑ" }, { name: "ΑΠΟΘΕΜΑΤΑ" }, { name: "ΒΡΑΧΥΠΡΟΘΕΣΜΕΣ ΥΠΟΧΡΕΩΣΕΙΣ" }, { name: "ΚΑΘΑΡΗ ΘΕΣΗ - ΠΡΟΒΛΕΨΕΙΣ -ΜΑΚΡ/ΣΜΕΣ ΥΠΟΧΡΕΩΣΕΙΣ" } ] },
        { id: 815, name: "Honduras - Plantilla de cuentas", path: "unverified/hn_cuentas_plantilla.json", nodeType: "db", pos: { x: 650, y: 950 }, icon: "🇭🇳", columns: [ { name: "Activo" }, { name: "Pasivo" }, { name: "Patrimonio" }, { name: "Egresos" }, { name: "Gastos" }, { name: "Ingresos" } ] },
        { id: 816, name: "Croatia - RRIF-ov računski plan", path: "unverified/hr_l10n_hr_chart_template_rrif.json", nodeType: "db", pos: { x: 950, y: 950 }, icon: "🇭🇷", columns: [ { name: "FINANCIJSKI REZULTAT POSLOVANJA" }, { name: "KAPITAL I PRIČUVE TE IZVANBILANČNI ZAPISI" }, { name: "KRATKOROČNE I DUGOROČNE OBVEZE..." } ] },
        { id: 817, name: "Italy - Generic Chart of Accounts", path: "unverified/it_l10n_it_chart_template_generic.json", nodeType: "db", pos: { x: 50, y: 1250 }, icon: "🇮🇹", columns: [ { name: "ATTIVO" }, { name: "CONTI DI RISULTATO" }, { name: "COSTI DELLA PRODUZIONE" }, { name: "IMPOSTE DELL'ESERCIZIO" }, { name: "PASSIVO" } ] },
        { id: 818, name: "Morocco - Compta Kazacube", path: "unverified/ma_l10n_kzc_temp_chart.json", nodeType: "db", pos: { x: 350, y: 1250 }, icon: "🇲🇦", columns: [ { name: "COMPTES DE BILAN" }, { name: "COMPTES DE GESTION" }, { name: "COMPTES DE RESULTATS" } ] },
        { id: 819, name: "Panama - Plan de Cuentas", path: "unverified/pa_l10npa_chart_template.json", nodeType: "db", pos: { x: 650, y: 1250 }, icon: "🇵🇦", columns: [ { name: "ACTIVOS" }, { name: "PASIVOS" }, { name: "PATRIMONIO" }, { name: "CUENTAS DE ORDEN ACREEDORAS" }, { name: "CUENTAS DE ORDEN DEUDORAS" } ] },
        { id: 820, name: "Peru - Plan de Cuentas", path: "unverified/pe_pe_chart_template.json", nodeType: "db", pos: { x: 950, y: 1250 }, icon: "🇵🇪", columns: [ { name: "Cuentas de Balance" }, { name: "Cuentas de Centros de Costo" }, { name: "Cuentas de Ganancias y Perdidas" }, { name: "CONTABILIDAD DE COSTOS (cont.)" } ] },
        { id: 821, name: "Poland - Plan kont", path: "unverified/pl_pl_chart_template.json", nodeType: "db", pos: { x: 50, y: 1550 }, icon: "🇵🇱", columns: [ { name: "Aktywa Trwałe" }, { name: "Kapitały własne i wynik finansowy" }, { name: "Koszty według rodzajów i ich rozliczenie" } ] },
        { id: 822, name: "Portugal - Template do Plano de Contas SNC", path: "unverified/pt_pt_chart_template.json", nodeType: "db", pos: { x: 350, y: 1550 }, icon: "🇵🇹", columns: [ { name: "Capital, reservas e resultados transitados" }, { name: "Contas a receber e a pagar" }, { name: "Gastos" }, { name: "Inventários e activos biológicos" } ] },
        { id: 823, name: "Romania - Chart of Accounts", path: "unverified/ro_ro_chart_template.json", nodeType: "db", pos: { x: 650, y: 1550 }, icon: "🇷🇴", columns: [ { name: "CONTURI FINANCIARE" }, { name: "CONTURI IN AFARA BILANTULUI" } ] },
        { id: 824, name: "Syscohada - Plan de compte", path: "unverified/syscohada_syscohada_chart_template.json", nodeType: "db", pos: { x: 950, y: 1550 }, icon: "🌍", columns: [ { name: "Comptes de bilan" }, { name: "Comptes de gestion" } ] }
    ],
    relationships: []
};

// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_9_571196tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 7</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 7
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Chart of Accounts (continued)
        { id: 901, name: "Thailand CoA", path: "unverified/th_chart.json", nodeType: "db", pos: { x: 50, y: 50 }, icon: "🇹🇭", columns: [ { name: "Assets" }, { name: "Liabilities" } ] },
        { id: 902, name: "Uruguay CoA", path: "unverified/uy_uy_chart_template.json", nodeType: "db", pos: { x: 50, y: 250 }, icon: "🇺🇾", columns: [ { name: "ACTIVO" }, { name: "PASIVO" } ] },
        { id: 903, name: "Venezuela CoA", path: "unverified/ve_ve_chart_template_amd.json", nodeType: "db", pos: { x: 50, y: 450 }, icon: "🇻🇪", columns: [ { name: "ACTIVO" }, { name: "PASIVO" } ] },

        // Core Accounting DocTypes
        { id: 904, name: "Item Tax Template", path: "doctype/item_tax_template/item_tax_template.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "🏷️", columns: [ { name: "validate()" }, { name: "autoname()" } ] },
        { id: 905, name: "Item Tax Template Schema", path: "doctype/item_tax_template/item_tax_template.json", nodeType: "db", pos: { x: 850, y: 50 }, icon: "📝", columns: [ { name: "title" }, { name: "company" }, { name: "taxes", type: "Table" } ] },
        { id: 906, name: "Budget", path: "doctype/budget/budget.py", nodeType: "code", pos: { x: 450, y: 300 }, icon: "🎯", columns: [ { name: "validate()" }, { name: "validate_expense_against_budget()" } ] },
        { id: 907, name: "Budget Schema", path: "doctype/budget/budget.json", nodeType: "db", pos: { x: 850, y: 300 }, icon: "📝", columns: [ { name: "budget_against" }, { name: "fiscal_year" }, { name: "accounts", type: "Table" } ] },
        { id: 908, name: "Payment Reconciliation Tool", path: "doctype/payment_reconciliation/payment_reconciliation.py", nodeType: "code", pos: { x: 450, y: 550 }, icon: "🤝", columns: [ { name: "get_unreconciled_entries()" }, { name: "allocate_entries()" }, { name: "reconcile()" } ] },
        { id: 909, name: "Payment Reconciliation UI", path: "doctype/payment_reconciliation/payment_reconciliation.js", nodeType: "ui", pos: { x: 50, y: 550 }, icon: "💻", columns: [ { name: "onload()" }, { name: "refresh()" }, { name: "reconcile()" } ] },

        // Tools
        { id: 910, name: "CoA Importer", path: "doctype/chart_of_accounts_importer/chart_of_accounts_importer.py", nodeType: "service", pos: { x: 450, y: 800 }, icon: "📥", columns: [ { name: "import_coa()" }, { name: "download_template()" }, { name: "get_coa() (for tree)" } ] },
        { id: 911, name: "Repost Accounting Ledger", path: "doctype/repost_accounting_ledger/repost_accounting_ledger.py", nodeType: "service", pos: { x: 850, y: 800 }, icon: "🔁", columns: [ { name: "on_submit() -> start_repost()" }, { name: "generate_preview()" } ] },

        // Core Projects DocTypes
        { id: 912, name: "Project", path: "doctype/project/project.py", nodeType: "code", pos: { x: 450, y: 1100 }, icon: "🏗️", columns: [ { name: "validate()" }, { name: "update_costing()" }, { name: "update_percent_complete()" } ] },
        { id: 913, name: "Project Schema", path: "doctype/project/project.json", nodeType: "db", pos: { x: 850, y: 1100 }, icon: "📝", columns: [ { name: "project_name" }, { name: "customer" }, { name: "status" }, { name: "users", type: "Table" } ] },
        { id: 914, name: "Task", path: "doctype/task/task.py", nodeType: "code", pos: { x: 450, y: 1350 }, icon: "✅", columns: [ { name: "validate()" }, { name: "update_project()" }, { name: "make_timesheet()" } ] },
        { id: 915, name: "Task Schema", path: "doctype/task/task.json", nodeType: "db", pos: { x: 850, y: 1350 }, icon: "📝", columns: [ { name: "subject" }, { name: "project" }, { name: "status" }, { name: "depends_on", type: "Table" } ] },
        { id: 916, name: "Timesheet", path: "doctype/timesheet/timesheet.py", nodeType: "code", pos: { x: 450, y: 1600 }, icon: "⏱️", columns: [ { name: "validate()" }, { name: "make_sales_invoice()" }, { name: "update_task_and_project()" } ] },
        { id: 917, name: "Timesheet Schema", path: "doctype/timesheet/timesheet.json", nodeType: "db", pos: { x: 850, y: 1600 }, icon: "📝", columns: [ { name: "employee" }, { name: "status" }, { name: "time_logs", type: "Table" } ] },
        
        // Reports
        { id: 918, name: "General Ledger Report", path: "report/general_ledger/general_ledger.py", nodeType: "code", pos: { x: 1250, y: 50 }, icon: "📊", columns: [ { name: "execute()" }, { name: "get_gl_entries()" } ] },
        { id: 919, name: "Trial Balance Report", path: "report/trial_balance/trial_balance.py", nodeType: "code", pos: { x: 1250, y: 300 }, icon: "📊", columns: [ { name: "execute()" }, { name: "get_opening_balances()" } ] },
        { id: 920, name: "Gross Profit Report", path: "report/gross_profit/gross_profit.py", nodeType: "code", pos: { x: 1250, y: 550 }, icon: "📊", columns: [ { name: "execute()" }, { name: "get_buying_amount()" } ] },
        { id: 921, name: "Accounts Receivable Report", path: "report/accounts_receivable/accounts_receivable.py", nodeType: "code", pos: { x: 1250, y: 800 }, icon: "📊", columns: [ { name: "execute()" }, { name: "get_invoice_details()" } ] },
        { id: 922, name: "Financial Statements", path: "report/financial_statements.py", nodeType: "code", pos: { x: 1650, y: 50 }, icon: "📚", columns: [ { name: "get_data()" }, { name: "set_gl_entries_by_account()" } ] },
        { id: 923, name: "GL Entry", path: "(Core DocType)", nodeType: "db", pos: { x: 1650, y: 400 }, icon: "🧾", columns: [ { name: "posting_date" }, { name: "account" }, { name: "debit" }, { name: "credit" } ] }
    ],
    relationships: [
        // Tool & Core Logic Interactions
        { from: { table: "CoA Importer" }, to: { table: "Account Logic", name: "(Core Account Creation)" }, type: "write" },
        { from: { table: "Repost Accounting Ledger" }, to: { table: "GL Entry" }, type: "write" },
        { from: { table: "Budget", column: "validate_expense_against_budget()" }, to: { table: "GL Entry" }, type: "read" },
        { from: { table: "Payment Reconciliation Tool", column: "get_unreconciled_entries()" }, to: { table: "GL Entry" }, type: "read" },
        { from: { table: "Payment Reconciliation Tool", column: "reconcile()" }, to: { table: "GL Entry" }, type: "write" },

        // Projects Module Interactions
        { from: { table: "Project", column: "copy_from_template()" }, to: { table: "Task" }, type: "write" },
        { from: { table: "Task", column: "update_project()" }, to: { table: "Project" }, type: "write" },
        { from: { table: "Timesheet", column: "update_task_and_project()" }, to: { table: "Task" }, type: "write" },
        { from: { table: "Timesheet", column: "update_task_and_project()" }, to: { table: "Project" }, type: "write" },
        { from: { table: "Timesheet", column: "make_sales_invoice()" }, to: { table: "SalesInvoice", name: "(Not in chunk)" }, type: "write" },
        { from: { table: "Task", column: "make_timesheet()" }, to: { table: "Timesheet" }, type: "write" },
        { from: { table: "Task Schema", column: "depends_on" }, to: { table: "Task Schema" } },

        // Report Interactions
        { from: { table: "General Ledger Report" }, to: { table: "GL Entry" }, type: "read" },
        { from: { table: "Trial Balance Report" }, to: { table: "GL Entry" }, type: "read" },
        { from: { table: "Accounts Receivable Report" }, to: { table: "GL Entry" }, type: "read" },
        { from: { table: "Gross Profit Report" }, to: { table: "SalesInvoice", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Financial Statements" }, to: { table: "GL Entry" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_10_582575tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Final Chunk
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Controllers
        { id: 1001, name: "AccountsController", path: "controllers/accounts_controller.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "🧾", columns: [ { name: "validate_due_date()" }, { name: "set_payment_schedule()" }, { name: "get_gl_dict()" } ] },
        { id: 1002, name: "StockController", path: "controllers/stock_controller.py", nodeType: "code", pos: { x: 850, y: 300 }, icon: "📦", columns: [ { name: "class StockController(AccountsController)" }, { name: "validate_warehouse()" }, { name: "update_stock_ledger()" }, { name: "make_gl_entries()" } ] },
        { id: 1003, name: "SellingController", path: "controllers/selling_controller.py", nodeType: "code", pos: { x: 1250, y: 550 }, icon: "📈", columns: [ { name: "class SellingController(StockController)" }, { name: "validate_selling_price()" }, { name: "set_gross_profit()" } ] },
        { id: 1004, name: "SubcontractingController", path: "controllers/subcontracting_controller.py", nodeType: "code", pos: { x: 850, y: 550 }, icon: "🏭", columns: [ { name: "class SubcontractingController(StockController)" }, { name: "get_available_materials()" }, { name: "create_raw_materials_supplied_or_received()" } ] },
        { id: 1005, name: "BuyingController", path: "controllers/buying_controller.py", nodeType: "code", pos: { x: 1250, y: 800 }, icon: "📉", columns: [ { name: "class BuyingController(SubcontractingController)" }, { name: "validate_for_subcontracting()" }, { name: "process_fixed_asset()" } ] },
        
        // Utility Controllers
        { id: 1006, name: "Taxes and Totals Calculator", path: "controllers/taxes_and_totals.py", nodeType: "code", pos: { x: 1650, y: 50 }, icon: "🔢", columns: [ { name: "calculate()" }, { name: "calculate_taxes()" }, { name: "apply_discount_amount()" } ] },
        { id: 1007, name: "Status Updater", path: "controllers/status_updater.py", nodeType: "code", pos: { x: 1650, y: 350 }, icon: "🔄", columns: [ { name: "update_prevdoc_status()" }, { name: "set_status()" } ] },
        { id: 1008, name: "Queries", path: "controllers/queries.py", nodeType: "code", pos: { x: 1650, y: 650 }, icon: "❓", columns: [ { name: "item_query()" }, { name: "employee_query()" }, { name: "warehouse_query()" } ] },
        
        // Setup DocTypes (Python Logic)
        { id: 1101, name: "Company Logic", path: "setup/doctype/company/company.py", nodeType: "code", pos: { x: 450, y: 1000 }, icon: "🏢", columns: [ { name: "create_default_accounts()" }, { name: "create_default_warehouses()" } ] },
        { id: 1102, name: "Item Group Logic", path: "setup/doctype/item_group/item_group.py", nodeType: "code", pos: { x: 450, y: 1250 }, icon: "📁", columns: [ { name: "class ItemGroup(NestedSet)" } ] },
        { id: 1103, name: "Employee Logic", path: "setup/doctype/employee/employee.py", nodeType: "code", pos: { x: 450, y: 1500 }, icon: "🧑‍💼", columns: [ { name: "create_user()" }, { name: "update_user_permissions()" } ] },
        { id: 1104, name: "Holiday List Logic", path: "setup/doctype/holiday_list/holiday_list.py", nodeType: "code", pos: { x: 450, y: 1750 }, icon: "📅", columns: [ { name: "get_weekly_off_dates()" }, { name: "get_local_holidays()" } ] },

        // Setup DocTypes (UI Logic)
        { id: 1201, name: "Company UI", path: "setup/doctype/company/company.js", nodeType: "ui", pos: { x: 2000, y: 1000 }, icon: "💻", columns: [ { name: "setup_queries()" }, { name: "delete_company_transactions()" } ] },
        { id: 1202, name: "Item Group UI", path: "setup/doctype/item_group/item_group.js", nodeType: "ui", pos: { x: 2000, y: 1250 }, icon: "💻", columns: [ { name: "refresh()" } ] },
        { id: 1203, name: "Employee UI", path: "setup/doctype/employee/employee.js", nodeType: "ui", pos: { x: 2000, y: 1500 }, icon: "💻", columns: [ { name: "create_user()" } ] },
        { id: 1204, name: "Holiday List UI", path: "setup/doctype/holiday_list/holiday_list.js", nodeType: "ui", pos: { x: 2000, y: 1750 }, icon: "💻", columns: [ { name: "get_weekly_off_dates()" } ] },
        
        // Setup DocTypes (Schema)
        { id: 1301, name: "Company Schema", path: "setup/doctype/company/company.json", nodeType: "db", pos: { x: 2350, y: 1000 }, icon: "📝", columns: [ { name: "default_currency" }, { name: "chart_of_accounts" } ] },
        { id: 1302, name: "Item Group Schema", path: "setup/doctype/item_group/item_group.json", nodeType: "db", pos: { x: 2350, y: 1250 }, icon: "📝", columns: [ { name: "parent_item_group" }, { name: "is_group" } ] },
        { id: 1303, name: "Employee Schema", path: "setup/doctype/employee/employee.json", nodeType: "db", pos: { x: 2350, y: 1500 }, icon: "📝", columns: [ { name: "user_id" }, { name: "reports_to" } ] },
        { id: 1304, name: "Holiday List Schema", path: "setup/doctype/holiday_list/holiday_list.json", nodeType: "db", pos: { x: 2350, y: 1750 }, icon: "📝", columns: [ { name: "weekly_off" }, { name: "country" } ] },
        
        // Setup Wizard & Demo Data
        { id: 1401, name: "Setup Wizard", path: "setup/setup_wizard/setup_wizard.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "🧙", columns: [ { name: "get_setup_stages()" }, { name: "setup_company()" } ] },
        { id: 1402, name: "Install Fixtures", path: "setup/setup_wizard/operations/install_fixtures.py", nodeType: "code", pos: { x: 50, y: 300 }, icon: "🛠️", columns: [ { name: "install()" }, { name: "install_company()" } ] },
        { id: 1403, name: "Setup Demo Data", path: "setup/demo.py", nodeType: "code", pos: { x: 50, y: 550 }, icon: "📊", columns: [ { name: "setup_demo_data()" }, { name: "create_transaction()" } ] },
        { id: 1404, name: "Demo Items", path: "setup/demo_data/item.json", nodeType: "db", pos: { x: 50, y: 800 }, icon: "📦", columns: [ { name: "SKU001" }, { name: "SKU002" } ] },
        { id: 1405, name: "Demo Sales Orders", path: "setup/demo_data/sales_order.json", nodeType: "db", pos: { x: 50, y: 1050 }, icon: "🧾", columns: [ { name: "customer: Grant Plastics" }, { name: "item: SKU004" } ] },
        { id: 1406, name: "Country Wise Tax Data", path: "setup/setup_wizard/data/country_wise_tax.json", nodeType: "db", pos: { x: 50, y: 1300 }, icon: "🌍", columns: [ { name: "Germany" }, { name: "France" } ] },

        // Patches
        { id: 1501, name: "Rename PO to WO Patch", path: "patches/v11_0/rename_production_order_to_work_order.py", nodeType: "service", pos: { x: 50, y: 1550 }, icon: "🔧", columns: [ { name: "rename_doc('Production Order', 'Work Order')" } ] },
        { id: 1502, name: "Migrate GL to PLE Patch", path: "patches/v14_0/migrate_gl_to_payment_ledger.py", nodeType: "service", pos: { x: 50, y: 1800 }, icon: "🔧", columns: [ { name: "insert_chunk_into_payment_ledger()" } ] },
        { id: 1503, name: "Delete Modules Patches", path: "patches/v14_0/delete_*_doctypes.py", nodeType: "service", pos: { x: 50, y: 2050 }, icon: "🗑️", columns: [ { name: "delete_doc('Module Def', 'Agriculture')" }, { name: "delete_doc('Module Def', 'Education')" } ] }

    ],
    relationships: [
        // Controller Inheritance
        { from: { table: "StockController" }, to: { table: "AccountsController" }, type: "flow" },
        { from: { table: "SubcontractingController" }, to: { table: "StockController" }, type: "flow" },
        { from: { table: "SellingController" }, to: { table: "StockController" }, type: "flow" },
        { from: { table: "BuyingController" }, to: { table: "SubcontractingController" }, type: "flow" },
        
        // Controllers using Utilities
        { from: { table: "SellingController" }, to: { table: "Taxes and Totals Calculator" }, type: "flow" },
        { from: { table: "BuyingController" }, to: { table: "Taxes and Totals Calculator" }, type: "flow" },
        { from: { table: "SellingController" }, to: { table: "Status Updater" }, type: "flow" },
        { from: { table: "BuyingController" }, to: { table: "Queries", column: "item_query()" } },
        
        // DocType MVC connections
        { from: { table: "Company UI" }, to: { table: "Company Logic" } },
        { from: { table: "Company Logic" }, to: { table: "Company Schema" }, type: "write" },
        { from: { table: "Item Group UI" }, to: { table: "Item Group Logic" } },
        { from: { table: "Item Group Logic" }, to: { table: "Item Group Schema" }, type: "write" },
        { from: { table: "Employee UI" }, to: { table: "Employee Logic" } },
        { from: { table: "Employee Logic" }, to: { table: "Employee Schema" }, type: "write" },
        { from: { table: "Holiday List UI" }, to: { table: "Holiday List Logic" } },
        { from: { table: "Holiday List Logic" }, to: { table: "Holiday List Schema" }, type: "write" },
        
        // Setup and Demo Data Flow
        { from: { table: "Setup Wizard" }, to: { table: "Install Fixtures" } },
        { from: { table: "Install Fixtures" }, to: { table: "Company Logic" }, type: "write" },
        { from: { table: "Install Fixtures" }, to: { table: "Country Wise Tax Data" }, type: "read" },
        { from: { table: "Setup Demo Data" }, to: { table: "Demo Items" }, type: "read" },
        { from: { table: "Setup Demo Data" }, to: { table: "Demo Sales Orders" }, type: "read" },

        // Patch Actions
        { from: { table: "Rename PO to WO Patch" }, to: { table: "SubcontractingController", name: "Work Order" }, type: "write" }, // Conceptually Work Order
        { from: { table: "Migrate GL to PLE Patch" }, to: { table: "AccountsController", name: "Payment Ledger" }, type: "write" }, // Conceptually Payment Ledger
        { from: { table: "Delete Modules Patches" }, to: { table: "Company Schema", name: "Module Def" }, type: "write" } // Conceptually Module Def
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_11_587756tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 11</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 11
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Patches
        { id: 1601, name: "Patch: Update Subscription to Auto Repeat", path: "patches/v10_1/transfer_subscription_to_auto_repeat.py", nodeType: "service", pos: { x: 50, y: 50 }, icon: "🔧", columns: [{ name: "Renames 'subscription' field to 'auto_repeat'" }, { name: "Migrates data from `Subscription` to `Auto Repeat`" }] },
        { id: 1602, name: "Patch: Add default buying/selling terms", path: "patches/v12_0/add_default_buying_selling_terms_in_company.py", nodeType: "service", pos: { x: 50, y: 300 }, icon: "🔧", columns: [{ name: "Updates `Company` with default terms" }] },
        { id: 1603, name: "Patch: Move Credit Limit to child table", path: "patches/v12_0/move_credit_limit_to_customer_credit_limit.py", nodeType: "service", pos: { x: 50, y: 500 }, icon: "🔧", columns: [{ name: "Migrates `Customer` credit limit to `Customer Credit Limit`" }] },
        { id: 1604, name: "Patch: Move Item Tax to template", path: "patches/v12_0/move_item_tax_to_item_tax_template.py", nodeType: "service", pos: { x: 50, y: 700 }, icon: "🔧", columns: [{ name: "Migrates `Item Tax` to `Item Tax Template`" }] },
        { id: 1605, name: "Patch: Rename Bank Reconciliation", path: "patches/v12_0/rename_bank_reconciliation.py", nodeType: "service", pos: { x: 50, y: 900 }, icon: "🔧", columns: [{ name: "Renames `Bank Reconciliation` to `Bank Clearance`" }] },
        { id: 1606, name: "Patch: Create Accounting Dimensions", path: "patches/v13_0/create_accounting_dimensions_in_orders.py", nodeType: "service", pos: { x: 50, y: 1100 }, icon: "🔧", columns: [{ name: "Adds custom fields for dimensions to Orders/Receipts" }] },
        { id: 1607, name: "Patch: Delete old reports", path: "patches/v13_0/delete_old_purchase_reports.py", nodeType: "service", pos: { x: 50, y: 1300 }, icon: "🗑️", columns: [{ name: "Deletes obsolete Purchase reports" }] },
        { id: 1608, name: "Patch: Repost incorrect SL/GL", path: "patches/v13_0/item_reposting_for_incorrect_sl_and_gl.py", nodeType: "service", pos: { x: 50, y: 1500 }, icon: "🔁", columns: [{ name: "Triggers reposting for `Stock Ledger Entry`" }] },
        { id: 1609, name: "Patch: Show Deprecation Warnings", path: "patches/v13_0/healthcare_deprecation_warning.py", nodeType: "service", pos: { x: 50, y: 1700 }, icon: "⚠️", columns: [{ name: "Prints warning for moved modules (Healthcare, HR, etc.)" }] },
        { id: 1610, name: "Patch: Create Advance Payment Ledger", path: "patches/v15_0/create_advance_payment_ledger_records.py", nodeType: "service", pos: { x: 50, y: 1900 }, icon: "🔧", columns: [{ name: "Creates `Advance Payment Ledger Entry` from `Payment Entry`" }] },
        { id: 1611, name: "Patch: Create Asset Depreciation Schedules", path: "patches/v15_0/create_asset_depreciation_schedules_from_assets.py", nodeType: "service", pos: { x: 50, y: 2100 }, icon: "🔧", columns: [{ name: "Migrates `Depreciation Schedule` to `Asset Depreciation Schedule`" }] },

        // Manufacturing Core
        { id: 1701, name: "BOM", path: "manufacturing/doctype/bom/bom.py", nodeType: "code", pos: { x: 450, y: 1000 }, icon: "📄", columns: [{ name: "class BOM(WebsiteGenerator)" }, { name: "validate()" }, { name: "on_submit()" }, { name: "update_cost()" }, { name: "get_exploded_items()" }, { name: "check_recursion()" }] },
        { id: 1702, name: "Work Order", path: "manufacturing/doctype/work_order/work_order.py", nodeType: "code", pos: { x: 850, y: 1200 }, icon: "🏗️", columns: [{ name: "class WorkOrder(Document)" }, { name: "on_submit()" }, { name: "on_cancel()" }, { name: "update_status()" }, { name: "create_job_card()" }] },
        { id: 1703, name: "Production Plan", path: "manufacturing/doctype/production_plan/production_plan.py", nodeType: "code", pos: { x: 450, y: 1500 }, icon: "📅", columns: [{ name: "class ProductionPlan(Document)" }, { name: "get_so_items()" }, { name: "make_work_order()" }, { name: "make_material_request()" }] },
        { id: 1704, name: "Job Card", path: "manufacturing/doctype/job_card/job_card.py", nodeType: "code", pos: { x: 1250, y: 1350 }, icon: "📋", columns: [{ name: "class JobCard(Document)" }, { name: "on_submit()" }, { name: "validate_time_logs()" }, { name: "set_status()" }] },
        { id: 1705, name: "Manufacturing Settings", path: "manufacturing/doctype/manufacturing_settings/manufacturing_settings.py", nodeType: "service", pos: { x: 450, y: 500 }, icon: "⚙️", columns: [{ name: "backflush_raw_materials_based_on" }, { name: "update_bom_costs_automatically" }, { name: "disable_capacity_planning" }] },
        { id: 1706, name: "Stock Entry", path: "(loaded from other chunk)", nodeType: "code", pos: { x: 1650, y: 1350 }, icon: "📦", columns: [{ name: "purpose: Material Transfer" }, { name: "purpose: Manufacture" }] },
        { id: 1707, name: "Sales Forecast", path: "manufacturing/doctype/sales_forecast/sales_forecast.py", nodeType: "code", pos: { x: 450, y: 2000 }, icon: "🔮", columns: [{ name: "generate_demand()" }, { name: "create_mps()" }] },
        { id: 1708, name: "Master Production Schedule", path: "manufacturing/doctype/master_production_schedule/master_production_schedule.py", nodeType: "code", pos: { x: 850, y: 2000 }, icon: " MASTER", columns: [{ name: "get_actual_demand()" }, { name: "make_mrp()" }] },
        { id: 1709, name: "BOM Update Tool", path: "manufacturing/doctype/bom_update_tool/bom_update_tool.py", nodeType: "code", pos: { x: 450, y: 2400 }, icon: "🔄", columns: [{ name: "enqueue_replace_bom()" }, { name: "enqueue_update_cost()" }] },
        { id: 1710, name: "BOM Update Log", path: "manufacturing/doctype/bom_update_log/bom_update_log.py", nodeType: "code", pos: { x: 850, y: 2400 }, icon: "📝", columns: [{ name: "process_boms_cost_level_wise()" }, { name: "resume_bom_cost_update_jobs()" }] },

        // Schemas
        { id: 1801, name: "BOM Schema", path: "doctype/bom/bom.json", nodeType: "db", pos: { x: 2050, y: 1000 }, icon: "📝", columns: [{ name: "items", type: "Table" }, { name: "operations", type: "Table" }, { name: "scrap_items", type: "Table" }] },
        { id: 1802, name: "Work Order Schema", path: "doctype/work_order/work_order.json", nodeType: "db", pos: { x: 2050, y: 1200 }, icon: "📝", columns: [{ name: "production_item" }, { name: "bom_no" }, { name: "required_items", type: "Table" }] },
        { id: 1803, name: "Production Plan Schema", path: "doctype/production_plan/production_plan.json", nodeType: "db", pos: { x: 2050, y: 1500 }, icon: "📝", columns: [{ name: "po_items", type: "Table" }, { name: "mr_items", type: "Table" }, { name: "sales_orders", type: "Table" }] },
        { id: 1804, name: "Job Card Schema", path: "doctype/job_card/job_card.json", nodeType: "db", pos: { x: 2050, y: 1350 }, icon: "📝", columns: [{ name: "work_order" }, { name: "operation" }, { name: "time_logs", type: "Table" }] },

        // UI
        { id: 1901, name: "BOM UI", path: "doctype/bom/bom.js", nodeType: "ui", pos: { x: 2450, y: 1000 }, icon: "💻", columns: [{ name: "update_cost()" }, { name: "make_work_order()" }] },
        { id: 1902, name: "Work Order UI", path: "doctype/work_order/work_order.js", nodeType: "ui", pos: { x: 2450, y: 1200 }, icon: "💻", columns: [{ name: "make_se()" }, { name: "make_job_card()" }] },
        { id: 1903, name: "Production Plan UI", path: "doctype/production_plan/production_plan.js", nodeType: "ui", pos: { x: 2450, y: 1500 }, icon: "💻", columns: [{ name: "get_items()" }, { name: "make_work_order()" }] },
        { id: 1904, name: "Manufacturing Workspace", path: "workspace/manufacturing.json", nodeType: "ui", pos: { x: 2450, y: 500 }, icon: "🏭", columns: [{ name: "Shortcuts (BOM, Work Order)" }, { name: "Reports & Masters" }] }
    ],
    relationships: [
        // Planning Flow
        { from: { table: "Sales Forecast" }, to: { table: "Master Production Schedule" }, type: "flow", label: "Creates" },
        { from: { table: "Master Production Schedule" }, to: { table: "Production Plan" }, type: "flow", label: "Can Create" }, // Implied flow
        { from: { table: "Production Plan UI" }, to: { table: "Production Plan" }, type: "flow" },
        { from: { table: "Production Plan", column: "get_so_items()" }, to: { table: "Sales Order" }, type: "read", label: "Reads" },
        { from: { table: "Production Plan", column: "make_work_order()" }, to: { table: "Work Order" }, type: "write", label: "Creates" },
        { from: { table: "Production Plan", column: "make_material_request()" }, to: { table: "Material Request" }, type: "write", label: "Creates" },

        // Execution Flow
        { from: { table: "Work Order UI" }, to: { table: "Work Order" }, type: "flow" },
        { from: { table: "Work Order", column: "get_items_and_operations_from_bom()" }, to: { table: "BOM" }, type: "read", label: "Uses" },
        { from: { table: "Work Order", column: "create_job_card()" }, to: { table: "Job Card" }, type: "write", label: "Creates" },
        { from: { table: "Work Order", column: "make_stock_entry()" }, to: { table: "Stock Entry" }, type: "write", label: "Creates" },
        { from: { table: "Job Card" }, to: { table: "Work Order" }, type: "read", label: "Updates" },
        { from: { table: "Job Card" }, to: { table: "Stock Entry" }, type: "write", label: "Can Create" },

        // BOM & Updates
        { from: { table: "BOM UI" }, to: { table: "BOM" }, type: "flow" },
        { from: { table: "BOM Update Tool" }, to: { table: "BOM Update Log" }, type: "write", label: "Creates" },
        { from: { table: "BOM Update Log", column: "process_boms_cost_level_wise()" }, to: { table: "BOM" }, type: "write", label: "Updates Cost" },
        { from: { table: "BOM Update Log", column: "run_replace_bom_job()" }, to: { table: "BOM" }, type: "write", label: "Replaces" },
        
        // Patches
        { from: { table: "Patch: Update Subscription to Auto Repeat" }, to: { table: "Auto Repeat" }, type: "write", label: "Migrates to" },
        { from: { table: "Patch: Create Accounting Dimensions" }, to: { table: "Sales Order" }, type: "write", label: "Modifies" },
        { from: { table: "Patch: Repost incorrect SL/GL" }, to: { table: "Stock Ledger Entry" }, type: "write", label: "Reposts" },
        { from: { table: "Patch: Create Advance Payment Ledger" }, to: { table: "Payment Entry" }, type: "read", label: "Reads From" },
        
        // MVC
        { from: { table: "BOM" }, to: { table: "BOM Schema" } },
        { from: { table: "Work Order" }, to: { table: "Work Order Schema" } },
        { from: { table: "Production Plan" }, to: { table: "Production Plan Schema" } },
        { from: { table: "Job Card" }, to: { table: "Job Card Schema" } }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_12_503984tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 12</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 12
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Onboarding Steps (UI/Guidance)
        { id: 2001, name: "Onboarding: Create Quotation", path: "setup/onboarding_step/create_a_quotation", nodeType: "ui", pos: { x: 50, y: 50 }, icon: "🎓", columns: [{ name: "Explains Quotation DocType" }] },
        { id: 2002, name: "Onboarding: Create Supplier", path: "setup/onboarding_step/create_a_supplier", nodeType: "ui", pos: { x: 50, y: 250 }, icon: "🎓", columns: [{ name: "Explains Supplier DocType" }] },
        { id: 2003, name: "Onboarding: Create Work Order", path: "manufacturing/onboarding_step/work_order", nodeType: "ui", pos: { x: 50, y: 450 }, icon: "🎓", columns: [{ name: "Explains Work Order DocType" }] },
        { id: 2004, name: "Onboarding: Create Item", path: "setup/onboarding_step/create_an_item", nodeType: "ui", pos: { x: 50, y: 650 }, icon: "🎓", columns: [{ name: "Explains Item DocType" }] },
        { id: 2005, name: "Onboarding: Create Purchase Order", path: "buying/onboarding_step/create_your_first_purchase_order", nodeType: "ui", pos: { x: 50, y: 850 }, icon: "🎓", columns: [{ name: "Explains Purchase Order DocType" }] },
        { id: 2006, name: "Onboarding: Financial Statements", path: "accounts/onboarding_step/financial_statements", nodeType: "ui", pos: { x: 50, y: 1050 }, icon: "🎓", columns: [{ name: "Explains Financial Reports" }] },
        { id: 2007, name: "Onboarding: Fixed Asset Accounts", path: "assets/onboarding_step/fixed_asset_accounts", nodeType: "ui", pos: { x: 50, y: 1250 }, icon: "🎓", columns: [{ name: "Explains Asset Accounts setup" }] },
        { id: 2008, name: "Onboarding: Production Planning", path: "manufacturing/onboarding_step/production_planning", nodeType: "ui", pos: { x: 50, y: 1450 }, icon: "🎓", columns: [{ name: "Explains Production Plan DocType" }] },
        { id: 2009, name: "Onboarding: Data Import", path: "setup/onboarding_step/data_import", nodeType: "ui", pos: { x: 50, y: 1650 }, icon: "🎓", columns: [{ name: "Explains Data Import Tool" }] },
        { id: 2010, name: "Onboarding: Stock Entry", path: "stock/onboarding_step/introduction_to_stock_entry", nodeType: "ui", pos: { x: 50, y: 1850 }, icon: "🎓", columns: [{ name: "Explains Stock Entry DocType" }] },
        { id: 2011, name: "Onboarding: Purchase an Asset", path: "assets/onboarding_step/asset_purchase", nodeType: "ui", pos: { x: 50, y: 2050 }, icon: "🎓", columns: [{ name: "Explains Asset purchasing cycle" }] },
        { id: 2012, name: "Onboarding: Sales Order", path: "selling/onboarding_step/sales_order", nodeType: "ui", pos: { x: 50, y: 2250 }, icon: "🎓", columns: [{ name: "Explains Sales Order DocType" }] },
        { id: 2013, name: "Onboarding: Setup a Company", path: "setup/onboarding_step/company_set_up", nodeType: "ui", pos: { x: 50, y: 2450 }, icon: "🎓", columns: [{ name: "Explains Company DocType" }] },
        { id: 2014, name: "Onboarding: Setup a Warehouse", path: "stock/onboarding_step/create_a_warehouse", nodeType: "ui", pos: { x: 50, y: 2650 }, icon: "🎓", columns: [{ name: "Explains Warehouse DocType" }] },
        { id: 2015, name: "Onboarding: Create Customer", path: "accounts/onboarding_step/create_a_customer", nodeType: "ui", pos: { x: 50, y: 2850 }, icon: "🎓", columns: [{ name: "Explains Customer DocType" }] },

        // Localization Service
        { id: 2101, name: "Localization Service", path: "erpnext/locale/", nodeType: "service", pos: { x: 450, y: 50 }, icon: "🌐", columns: [{ name: "Provides translations for UI text" }, { name: "Languages: ar, bs, cs, da, de, es..." }] },

        // Referenced Core DocTypes (assuming they exist from other chunks)
        { id: 101, name: "Quotation", path: "selling/doctype/quotation", nodeType: "code", pos: { x: 850, y: 50 }, icon: "📄" },
        { id: 102, name: "Supplier", path: "buying/doctype/supplier", nodeType: "code", pos: { x: 850, y: 250 }, icon: "🏭" },
        { id: 1702, name: "Work Order", path: "manufacturing/doctype/work_order", nodeType: "code", pos: { x: 850, y: 450 }, icon: "🏗️" },
        { id: 103, name: "Item", path: "stock/doctype/item", nodeType: "code", pos: { x: 850, y: 650 }, icon: "📦" },
        { id: 104, name: "Purchase Order", path: "buying/doctype/purchase_order", nodeType: "code", pos: { x: 850, y: 850 }, icon: "🛒" },
        { id: 105, name: "Account", path: "accounts/doctype/account", nodeType: "code", pos: { x: 850, y: 1250 }, icon: "🏛️" },
        { id: 1703, name: "Production Plan", path: "manufacturing/doctype/production_plan", nodeType: "code", pos: { x: 850, y: 1450 }, icon: "📅" },
        { id: 106, name: "Stock Entry", path: "stock/doctype/stock_entry", nodeType: "code", pos: { x: 850, y: 1850 }, icon: "➡️" },
        { id: 107, name: "Sales Order", path: "selling/doctype/sales_order", nodeType: "code", pos: { x: 850, y: 2250 }, icon: "📈" },
        { id: 1101, name: "Company", path: "setup/doctype/company", nodeType: "code", pos: { x: 850, y: 2450 }, icon: "🏢" },
        { id: 108, name: "Warehouse", path: "stock/doctype/warehouse", nodeType: "code", pos: { x: 850, y: 2650 }, icon: "🏠" },
        { id: 109, name: "Customer", path: "selling/doctype/customer", nodeType: "code", pos: { x: 850, y: 2850 }, icon: "🧑" },

        // Referenced Reports and Tools
        { id: 922, name: "Financial Statements", path: "report/financial_statements", nodeType: "code", pos: { x: 850, y: 1050 }, icon: "📊" },
        { id: 110, name: "Data Import Tool", path: "core/doctype/data_import", nodeType: "service", pos: { x: 850, y: 1650 }, icon: "📥" }
    ],
    relationships: [
        // Onboarding Step -> DocType relationships
        { from: { table: "Onboarding: Create Quotation" }, to: { table: "Quotation" }, type: "read" },
        { from: { table: "Onboarding: Create Supplier" }, to: { table: "Supplier" }, type: "read" },
        { from: { table: "Onboarding: Create Work Order" }, to: { table: "Work Order" }, type: "read" },
        { from: { table: "Onboarding: Create Item" }, to: { table: "Item" }, type: "read" },
        { from: { table: "Onboarding: Create Purchase Order" }, to: { table: "Purchase Order" }, type: "read" },
        { from: { table: "Onboarding: Financial Statements" }, to: { table: "Financial Statements" }, type: "read" },
        { from: { table: "Onboarding: Fixed Asset Accounts" }, to: { table: "Account" }, type: "read" },
        { from: { table: "Onboarding: Production Planning" }, to: { table: "Production Plan" }, type: "read" },
        { from: { table: "Onboarding: Data Import" }, to: { table: "Data Import Tool" }, type: "read" },
        { from: { table: "Onboarding: Stock Entry" }, to: { table: "Stock Entry" }, type: "read" },
        { from: { table: "Onboarding: Purchase an Asset" }, to: { table: "Purchase Order" }, type: "read" },
        { from: { table: "Onboarding: Sales Order" }, to: { table: "Sales Order" }, type: "read" },
        { from: { table: "Onboarding: Setup a Company" }, to: { table: "Company" }, type: "read" },
        { from: { table: "Onboarding: Setup a Warehouse" }, to: { table: "Warehouse" }, type: "read" },
        { from: { table: "Onboarding: Create Customer" }, to: { table: "Customer" }, type: "read" },
        
        // Localization Service -> UI/Schema relationships
        { from: { table: "Localization Service" }, to: { table: "Sales Order Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Delivery Note Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Purchase Receipt Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Project Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Task Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "BOM Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Company Schema", name: "(Not in chunk)" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Item Schema", name: "(Not in chunk)" }, type: "read" }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_13_494277tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 13</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 13: Localization & Onboarding
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Localization Service
        { id: 2201, name: "Localization Service", path: "erpnext/locale/", nodeType: "service", pos: { x: 450, y: 100 }, icon: "🌐", columns: [
            { name: "Translation Template (main.pot)" },
            { name: "Spanish (es.po)" },
            { name: "Farsi (fa.po)" },
            { name: "Finnish (fi.po)" },
            { name: "French (fr.po)" },
            { name: "Croatian (hr.po)" },
            { name: "Hungarian (hu.po)" },
            { name: "Indonesian (id.po)" },
            { name: "Italian (it.po)" }
        ]},

        // Onboarding Steps (UI/Guidance)
        { id: 2001, name: "Onboarding: Create Quotation", path: "setup/onboarding_step/create_a_quotation.json", nodeType: "ui", pos: { x: 50, y: 500 }, icon: "🎓", columns: [{ name: "Explains Quotation DocType" }] },
        { id: 2002, name: "Onboarding: Create Supplier", path: "setup/onboarding_step/create_a_supplier.json", nodeType: "ui", pos: { x: 50, y: 750 }, icon: "🎓", columns: [{ name: "Explains Supplier DocType" }] },
        { id: 2003, name: "Onboarding: Create Work Order", path: "manufacturing/onboarding_step/work_order.json", nodeType: "ui", pos: { x: 50, y: 1000 }, icon: "🎓", columns: [{ name: "Explains Work Order DocType" }] },
        { id: 2004, name: "Onboarding: Create Item", path: "setup/onboarding_step/create_an_item.json", nodeType: "ui", pos: { x: 50, y: 1250 }, icon: "🎓", columns: [{ name: "Explains Item DocType" }] },
        { id: 2005, name: "Onboarding: Create Purchase Order", path: "buying/onboarding_step/create_your_first_purchase_order.json", nodeType: "ui", pos: { x: 50, y: 1500 }, icon: "🎓", columns: [{ name: "Explains Purchase Order DocType" }] },
        { id: 2013, name: "Onboarding: Setup Company", path: "setup/onboarding_step/company_set_up.json", nodeType: "ui", pos: { x: 50, y: 1750 }, icon: "🎓", columns: [{ name: "Explains Company DocType" }] },
        { id: 2014, name: "Onboarding: Setup Warehouse", path: "stock/onboarding_step/create_a_warehouse.json", nodeType: "ui", pos: { x: 50, y: 2000 }, icon: "🎓", columns: [{ name: "Explains Warehouse DocType" }] },

        // Representative Core DocTypes
        { id: 303, name: "Sales Invoice UI", path: "accounts/doctype/sales_invoice/sales_invoice.js", nodeType: "ui", pos: { x: 850, y: 50 }, icon: "💻", columns: [{ name: "Label: 'Customer'" }, { name: "Button: 'Save'" }] },
        { id: 111, name: "Item Schema", path: "stock/doctype/item/item.json", nodeType: "db", pos: { x: 850, y: 300 }, icon: "📝", columns: [{ name: "field: 'item_name'" }, { name: "field: 'description'" }] },
        { id: 1902, name: "Work Order UI", path: "manufacturing/doctype/work_order/work_order.js", nodeType: "ui", pos: { x: 850, y: 550 }, icon: "🏭", columns: [{ name: "Label: 'Production Item'" }] },
        { id: 109, name: "Customer UI", path: "selling/doctype/customer/customer.js", nodeType: "ui", pos: { x: 850, y: 800 }, icon: "🧑", columns: [{ name: "Label: 'Customer Name'" }] },
        { id: 1101, name: "Company Schema", path: "setup/doctype/company/company.json", nodeType: "db", pos: { x: 850, y: 1050 }, icon: "🏢", columns: [{ name: "field: 'company_name'" }] }
    ],
    relationships: [
        // Onboarding steps point to the doctypes they explain
        { from: { table: "Onboarding: Create Quotation" }, to: { table: "Sales Invoice UI" } }, // Conceptually linked
        { from: { table: "Onboarding: Create Supplier" }, to: { table: "Customer UI" } }, // Supplier/Customer are both parties
        { from: { table: "Onboarding: Create Work Order" }, to: { table: "Work Order UI" } },
        { from: { table: "Onboarding: Create Item" }, to: { table: "Item Schema" } },
        { from: { table: "Onboarding: Setup Company" }, to: { table: "Company Schema" } },

        // Localization Service provides translations for all UI and Schema labels
        { from: { table: "Localization Service" }, to: { table: "Sales Invoice UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Item Schema" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Work Order UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Customer UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Company Schema" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Onboarding: Create Quotation" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Onboarding: Create Supplier" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Onboarding: Create Work Order" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_14_496569tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 14</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 14: Localization
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Central Localization Service Node
        { id: 2301, name: "Localization Service", path: "erpnext/locale/", nodeType: "service", pos: { x: 450, y: 50 }, icon: "🌐", columns: [
            { name: "Norwegian (nb.po)" },
            { name: "Dutch (nl.po)" },
            { name: "Polish (pl.po)" },
            { name: "Portuguese (pt.po)" },
            { name: "Brazilian Portuguese (pt-BR.po)" },
            { name: "Russian (ru.po)" }
        ]},

        // Representative UI and Schema components that are translated
        { id: 2302, name: "Sales Order UI", path: "selling/doctype/sales_order/sales_order.js", nodeType: "ui", pos: { x: 850, y: 50 }, icon: "💻", columns: [
            { name: "Label: '% Delivered'" },
            { name: "msgid \"%  Delivered\"" }
        ]},
        { id: 2303, name: "BOM UI", path: "public/js/bom_configurator/bom_configurator.bundle.js", nodeType: "ui", pos: { x: 850, y: 300 }, icon: "🏭", columns: [
            { name: "Label: 'Raw Material'" },
            { name: "msgid \" Raw Material\"" }
        ]},
        { id: 2304, name: "Item Logic", path: "stock/doctype/item/item.py", nodeType: "code", pos: { x: 850, y: 550 }, icon: "🐍", columns: [
            { name: "Error Message" },
            { name: "msgid \"'Has Serial No' can not be 'Yes' for non-stock item\"" }
        ]},
        { id: 2305, name: "Project Schema", path: "projects/doctype/project/project.json", nodeType: "db", pos: { x: 850, y: 800 }, icon: "📝", columns: [
            { name: "field: 'percent_complete_method'" },
            { name: "msgid \"% Complete Method\"" }
        ]},
        { id: 2306, name: "Sales Analytics Report", path: "selling/report/sales_analytics/sales_analytics.py", nodeType: "code", pos: { x: 850, y: 1050 }, icon: "📊", columns: [
            { name: "Column: 'Name'" },
            { name: "msgid \" Name\"" }
        ]}
    ],
    relationships: [
        // The Localization Service provides translations FOR various UI/Schema/Code components
        { from: { table: "Localization Service" }, to: { table: "Sales Order UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "BOM UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Item Logic" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Project Schema" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Sales Analytics Report" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_15_499457tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Chunk 15</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 15: Localization
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Central Localization Service Node
        { id: 2401, name: "Localization Service", path: "erpnext/locale/", nodeType: "service", pos: { x: 450, y: 100 }, icon: "🌐", columns: [
            { name: "Serbian (Cyrillic) (sr.po)" },
            { name: "Serbian (Latin) (sr_CS.po)" },
            { name: "Swedish (sv.po)" },
            { name: "Tamil (ta.po)" },
            { name: "Thai (th.po)" },
            { name: "Turkish (tr.po)" },
            { name: "Vietnamese (vi.po)" }
        ]},

        // Representative UI and Schema components that are translated
        { id: 2302, name: "Sales Order UI", path: "selling/doctype/sales_order/sales_order.js", nodeType: "ui", pos: { x: 850, y: 50 }, icon: "💻", columns: [
            { name: "msgid \"%  Delivered\"" },
            { name: "msgstr \"% Isporučeno\"" }
        ]},
        { id: 2303, name: "BOM Configurator UI", path: "public/js/bom_configurator/bom_configurator.bundle.js", nodeType: "ui", pos: { x: 850, y: 300 }, icon: "🏭", columns: [
            { name: "msgid \" Raw Material\"" },
            { name: "msgstr \" Sirovina\"" }
        ]},
        { id: 2304, name: "Item Logic", path: "stock/doctype/item/item.py", nodeType: "code", pos: { x: 850, y: 550 }, icon: "🐍", columns: [
            { name: "msgid \"'Has Serial No' can not be 'Yes' for non-stock item\"" },
            { name: "msgstr \"'Ima serijski broj' ne može biti 'Da' za stavke van zaliha\"" }
        ]},
        { id: 2305, name: "Project Schema", path: "projects/doctype/project/project.json", nodeType: "db", pos: { x: 850, y: 800 }, icon: "📝", columns: [
            { name: "msgid \"% Complete Method\"" },
            { name: "msgstr \"% Metod izvršenja\"" }
        ]},
        { id: 2306, name: "Sales Analytics Report", path: "selling/report/sales_analytics/sales_analytics.py", nodeType: "code", pos: { x: 850, y: 1050 }, icon: "📊", columns: [
            { name: "msgid \" Name\"" },
            { name: "msgstr \" Naziv\"" }
        ]}
    ],
    relationships: [
        // The Localization Service provides translations FOR various UI/Schema/Code components
        { from: { table: "Localization Service" }, to: { table: "Sales Order UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "BOM Configurator UI" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Item Logic" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Project Schema" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Sales Analytics Report" }, type: "read" }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_16_569209tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Chunk 16
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Controllers
        { id: 2501, name: "AccountsController", path: "controllers/accounts_controller.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "🧾", columns: [{ name: "validate_due_date()" }, { name: "get_gl_dict()" }] },
        { id: 2502, name: "StockController", path: "controllers/stock_controller.py", nodeType: "code", pos: { x: 50, y: 300 }, icon: "📦", columns: [{ name: "class StockController(AccountsController)" }, { name: "update_stock_ledger()" }] },
        { id: 2503, name: "SellingController", path: "controllers/selling_controller.py", nodeType: "code", pos: { x: 50, y: 550 }, icon: "📈", columns: [{ name: "class SellingController(StockController)" }] },
        { id: 2504, name: "BuyingController", path: "controllers/buying_controller.py", nodeType: "code", pos: { x: 50, y: 800 }, icon: "📉", columns: [{ name: "class BuyingController(...)" }] },

        // Plaid Integration
        { id: 2601, name: "Plaid Settings UI", path: "doctype/plaid_settings/plaid_settings.js", nodeType: "ui", pos: { x: 450, y: 50 }, icon: "💻", columns: [{ name: "Link a new bank account" }, { name: "Sync Now" }] },
        { id: 2602, name: "Plaid Settings Logic", path: "doctype/plaid_settings/plaid_settings.py", nodeType: "code", pos: { x: 850, y: 50 }, icon: "⚙️", columns: [{ name: "get_link_token()" }, { name: "enqueue_synchronization()" }] },
        { id: 2603, name: "Plaid Connector", path: "doctype/plaid_settings/plaid_connector.py", nodeType: "code", pos: { x: 1250, y: 50 }, icon: "🔌", columns: [{ name: "class PlaidConnector" }, { name: "get_access_token()" }, { name: "get_transactions()" }] },
        { id: 2604, name: "Plaid API Service", path: "(external)", nodeType: "service", pos: { x: 1650, y: 50 }, icon: "🌐", columns: [{ name: "plaid.Client()" }] },

        // Buying Module
        { id: 2701, name: "Supplier", path: "doctype/supplier/supplier.py", nodeType: "code", pos: { x: 450, y: 400 }, icon: "🏭", columns: [{ name: "validate()" }, { name: "get_supplier_group_details()" }] },
        { id: 2702, name: "Request for Quotation", path: "doctype/request_for_quotation/request_for_quotation.py", nodeType: "code", pos: { x: 850, y: 400 }, icon: "❓", columns: [{ name: "make_supplier_quotation_from_rfq()" }] },
        { id: 2703, name: "Supplier Quotation", path: "doctype/supplier_quotation/supplier_quotation.py", nodeType: "code", pos: { x: 1250, y: 400 }, icon: "📝", columns: [{ name: "make_purchase_order()" }] },
        { id: 2704, name: "Purchase Order", path: "doctype/purchase_order/purchase_order.py", nodeType: "code", pos: { x: 1650, y: 400 }, icon: "🛒", columns: [{ name: "make_purchase_receipt()" }, { name: "make_purchase_invoice()" }] },

        // CRM Module
        { id: 2801, name: "Lead", path: "doctype/lead/lead.py", nodeType: "code", pos: { x: 450, y: 800 }, icon: "👤", columns: [{ name: "make_customer()" }, { name: "make_opportunity()" }] },
        { id: 2802, name: "Opportunity", path: "doctype/opportunity/opportunity.py", nodeType: "code", pos: { x: 850, y: 800 }, icon: "💡", columns: [{ name: "make_quotation()" }] },
        { id: 2803, name: "Prospect", path: "doctype/prospect/prospect.py", nodeType: "code", pos: { x: 450, y: 1100 }, icon: "🏢", columns: [{ name: "make_customer()" }, { name: "make_opportunity()" }] },
        { id: 2804, name: "Contract", path: "doctype/contract/contract.py", nodeType: "code", pos: { x: 1250, y: 800 }, icon: "📜", columns: [{ name: "update_contract_status()" }] },

        // Assets Module
        { id: 2901, name: "Asset Repair", path: "doctype/asset_repair/asset_repair.py", nodeType: "code", pos: { x: 450, y: 1400 }, icon: "🛠️", columns: [{ name: "make_gl_entries()" }, { name: "decrease_stock_quantity()" }] },
        { id: 2902, name: "Asset Capitalization", path: "doctype/asset_capitalization/asset_capitalization.py", nodeType: "code", pos: { x: 850, y: 1400 }, icon: "🏗️", columns: [{ name: "make_gl_entries()" }, { name: "update_stock_ledger()" }] },
        { id: 2903, name: "Asset Value Adjustment", path: "doctype/asset_value_adjustment/asset_value_adjustment.py", nodeType: "code", pos: { x: 1250, y: 1400 }, icon: "💲", columns: [{ name: "make_asset_revaluation_entry()" }] },
        { id: 2904, name: "Asset (Master)", path: "doctype/asset/asset.py", nodeType: "db", pos: { x: 850, y: 1700 }, icon: "💻", columns: [{ name: "status" }, { name: "value_after_depreciation" }] },

        // Localization
        { id: 3001, name: "Localization Service", path: "erpnext/locale/", nodeType: "service", pos: { x: 2000, y: 800 }, icon: "🌐", columns: [{ name: "Chinese (zh.po)" }, { name: "Chinese Traditional (zh_TW.po)" }] }
    ],
    relationships: [
        // Controller Inheritance
        { from: { table: "StockController" }, to: { table: "AccountsController" }, type: "flow" },
        { from: { table: "SellingController" }, to: { table: "StockController" }, type: "flow" },
        { from: { table: "BuyingController" }, to: { table: "StockController" }, type: "flow" }, // Simplified for clarity

        // Plaid Integration Flow
        { from: { table: "Plaid Settings UI" }, to: { table: "Plaid Settings Logic" }, type: "flow" },
        { from: { table: "Plaid Settings Logic" }, to: { table: "Plaid Connector" }, type: "flow" },
        { from: { table: "Plaid Connector" }, to: { table: "Plaid API Service" }, type: "read" },

        // Buying Flow
        { from: { table: "Request for Quotation" }, to: { table: "Supplier Quotation" }, type: "write" },
        { from: { table: "Supplier Quotation" }, to: { table: "Purchase Order" }, type: "write" },
        { from: { table: "Supplier" }, to: { table: "Request for Quotation" }, type: "read" },

        // CRM Flow
        { from: { table: "Lead" }, to: { table: "Opportunity" }, type: "write" },
        { from: { table: "Lead" }, to: { table: "Prospect" }, type: "write" },
        { from: { table: "Prospect" }, to: { table: "Opportunity" }, type: "write" },
        { from: { table: "Opportunity" }, to: { table: "Quotation", name: "(Not in chunk)" }, type: "write" },

        // Assets Flow
        { from: { table: "Asset Repair" }, to: { table: "Asset (Master)" }, type: "write" },
        { from: { table: "Asset Capitalization" }, to: { table: "Asset (Master)" }, type: "write" },
        { from: { table: "Asset Value Adjustment" }, to: { table: "Asset (Master)" }, type: "write" },

        // Localization
        { from: { table: "Localization Service" }, to: { table: "Purchase Order" }, type: "read" },
        { from: { table: "Localization Service" }, to: { table: "Lead" }, type: "read" }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_17_582918tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Final Chunk
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Controllers
        { id: 2501, name: "AccountsController", path: "controllers/accounts_controller.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "🧾" },
        { id: 2502, name: "StockController", path: "controllers/stock_controller.py", nodeType: "code", pos: { x: 450, y: 300 }, icon: "📦" },
        { id: 2503, name: "SellingController", path: "controllers/selling_controller.py", nodeType: "code", pos: { x: 450, y: 550 }, icon: "📈" },
        { id: 2504, name: "BuyingController", path: "controllers/buying_controller.py", nodeType: "code", pos: { x: 450, y: 800 }, icon: "📉" },
        { id: 2505, name: "TransactionBase", path: "utilities/transaction_base.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "🏗️" },

        // Integrations
        { id: 2601, name: "Plaid Integration", path: "integrations/plaid_integration.py", nodeType: "code", pos: { x: 850, y: 50 }, icon: "🏦" },
        
        // Modules (Buying, CRM, Assets)
        { id: 2701, name: "Request for Quotation", path: "buying/doctype/request_for_quotation/request_for_quotation.py", nodeType: "code", pos: { x: 850, y: 400 }, icon: "❓" },
        { id: 2702, name: "Supplier Quotation", path: "buying/doctype/supplier_quotation/supplier_quotation.py", nodeType: "code", pos: { x: 1250, y: 400 }, icon: "📝" },
        { id: 2703, name: "Purchase Order", path: "buying/doctype/purchase_order/purchase_order.py", nodeType: "code", pos: { x: 1650, y: 400 }, icon: "🛒" },
        { id: 2801, name: "Lead", path: "crm/doctype/lead/lead.py", nodeType: "code", pos: { x: 850, y: 800 }, icon: "👤" },
        { id: 2802, name: "Opportunity", path: "crm/doctype/opportunity/opportunity.py", nodeType: "code", pos: { x: 1250, y: 800 }, icon: "💡" },
        { id: 2803, name: "Contract", path: "crm/doctype/contract/contract.py", nodeType: "code", pos: { x: 1650, y: 800 }, icon: "📜" },
        { id: 2901, name: "Asset", path: "assets/doctype/asset/asset.py", nodeType: "code", pos: { x: 850, y: 1400 }, icon: "💻" },
        { id: 2902, name: "Asset Repair", path: "assets/doctype/asset_repair/asset_repair.py", nodeType: "code", pos: { x: 450, y: 1400 }, icon: "🛠️" },
        { id: 2903, name: "Asset Depreciation", path: "assets/doctype/asset/depreciation.py", nodeType: "code", pos: { x: 1250, y: 1400 }, icon: "📉" },
        { id: 2904, name: "Asset Maintenance", path: "maintenance/doctype/asset_maintenance/asset_maintenance.py", nodeType: "code", pos: { x: 450, y: 1700 }, icon: "🔧" },
        { id: 2905, name: "Maintenance Schedule", path: "maintenance/doctype/maintenance_schedule/maintenance_schedule.py", nodeType: "code", pos: { x: 850, y: 1700 }, icon: "📅" },
        { id: 2906, name: "Maintenance Visit", path: "maintenance/doctype/maintenance_visit/maintenance_visit.py", nodeType: "code", pos: { x: 1250, y: 1700 }, icon: "👨‍🔧" },
        
        // Utilities & Startup
        { id: 1401, name: "Setup Wizard", path: "setup/setup_wizard/setup_wizard.py", nodeType: "service", pos: { x: 50, y: 1100 }, icon: "🧙" },
        { id: 1500, name: "Boot Session", path: "startup/boot.py", nodeType: "service", pos: { x: 50, y: 1400 }, icon: "🚀" },
        { id: 3001, name: "Bulk Transaction Processing", path: "utilities/bulk_transaction.py", nodeType: "service", pos: { x: 50, y: 1700 }, icon: "🔄" },
        
        // Regional
        { id: 3101, name: "Italy Setup", path: "regional/italy/setup.py", nodeType: "service", pos: { x: 2000, y: 50 }, icon: "🇮🇹" },
        { id: 3102, name: "UAE Setup", path: "regional/united_arab_emirates/setup.py", nodeType: "service", pos: { x: 2000, y: 300 }, icon: "🇦🇪" },
        { id: 3103, name: "USA Setup (IRS 1099)", path: "regional/united_states/setup.py", nodeType: "service", pos: { x: 2000, y: 550 }, icon: "🇺🇸" },
        
        // UI Components
        { id: 3201, name: "Transaction JS Controller", path: "public/js/controllers/transaction.js", nodeType: "ui", pos: { x: 2350, y: 50 }, icon: "💻" },
        { id: 3202, name: "Serial/Batch Selector", path: "public/js/utils/serial_no_batch_selector.js", nodeType: "ui", pos: { x: 2350, y: 300 }, icon: "🔢" },
        { id: 3203, name: "Ledger Preview", path: "public/js/utils/ledger_preview.js", nodeType: "ui", pos: { x: 2350, y: 550 }, icon: "📊" }
    ],
    relationships: [
        // Controller Inheritance
        { from: { table: "AccountsController" }, to: { table: "TransactionBase" }, type: "flow" },
        { from: { table: "StockController" }, to: { table: "AccountsController" }, type: "flow" },
        { from: { table: "SellingController" }, to: { table: "StockController" }, type: "flow" },
        { from: { table: "BuyingController" }, to: { table: "StockController" }, type: "flow" },

        // UI -> Controller
        { from: { table: "Transaction JS Controller" }, to: { table: "StockController" }, type: "read" },
        
        // Integrations
        { from: { table: "Plaid Integration" }, to: { table: "AccountsController" }, type: "flow" },
        
        // Buying Flow
        { from: { table: "Request for Quotation" }, to: { table: "Supplier Quotation" }, type: "write" },
        { from: { table: "Supplier Quotation" }, to: { table: "Purchase Order" }, type: "write" },
        { from: { table: "Purchase Order" }, to: { table: "BuyingController" }, type: "flow" },
        
        // CRM Flow
        { from: { table: "Lead" }, to: { table: "Opportunity" }, type: "write" },
        { from: { table: "Opportunity" }, to: { table: "Contract" }, type: "flow" },
        
        // Assets Flow
        { from: { table: "Asset Repair" }, to: { table: "Asset" }, type: "write" },
        { from: { table: "Asset Depreciation" }, to: { table: "Asset" }, type: "write" },
        { from: { table: "Asset" }, to: { table: "StockController" }, type: "flow" },
        
        // Maintenance Flow
        { from: { table: "Maintenance Schedule" }, to: { table: "Asset Maintenance" }, type: "read" },
        { from: { table: "Maintenance Visit" }, to: { table: "Maintenance Schedule" }, type: "read" },
        
        // Regional Setups
        { from: { table: "Italy Setup" }, to: { table: "AccountsController" }, type: "flow" },
        { from: { table: "UAE Setup" }, to: { table: "AccountsController" }, type: "flow" },
        { from: { table: "USA Setup (IRS 1099)" }, to: { table: "BuyingController" }, type: "flow" },
        
        // Utility Connections
        { from: { table: "Setup Wizard" }, to: { table: "Boot Session" }, type: "flow" },
        { from: { table: "Bulk Transaction Processing" }, to: { table: "TransactionBase" }, type: "flow" },
        { from: { table: "Serial/Batch Selector" }, to: { table: "Transaction JS Controller" }, type: "read" },
        { from: { table: "Ledger Preview" }, to: { table: "Transaction JS Controller" }, type: "read" }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_18_585141tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Final Chunk
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Stock Logic
        { id: 3001, name: "Stock Ledger", path: "stock/stock_ledger.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "📚", columns: [{ name: "make_sl_entries()" }, { name: "repost_future_sle()" }, { name: "update_entries_after" }] },
        { id: 3002, name: "Stock Balance", path: "stock/stock_balance.py", nodeType: "code", pos: { x: 50, y: 350 }, icon: "⚖️", columns: [{ name: "repost_stock()" }, { name: "get_reserved_qty()" }, { name: "get_ordered_qty()" }] },
        { id: 3003, name: "Serial/Batch Bundle Logic", path: "stock/serial_batch_bundle.py", nodeType: "code", pos: { x: 450, y: 650 }, icon: "📦", columns: [{ name: "SerialBatchBundle" }, { name: "SerialBatchCreation" }] },
        { id: 3004, name: "Item Details Getter", path: "stock/get_item_details.py", nodeType: "code", pos: { x: 50, y: 650 }, icon: "🔍", columns: [{ name: "get_item_details()" }, { name: "get_price_list_rate()" }] },
        { id: 3005, name: "Valuation Logic", path: "stock/valuation.py", nodeType: "code", pos: { x: 450, y: 350 }, icon: "💲", columns: [{ name: "FIFOValuation" }, { name: "LIFOValuation" }] },
        { id: 3006, name: "Auto Reorder Logic", path: "stock/reorder_item.py", nodeType: "code", pos: { x: 50, y: 950 }, icon: "🔄", columns: [{ name: "reorder_item()" }, { name: "create_material_request()" }] },

        // Core Transactional DocTypes
        { id: 3101, name: "Stock Entry", path: "doctype/stock_entry/stock_entry.py", nodeType: "code", pos: { x: 850, y: 50 }, icon: "➡️", columns: [{ name: "update_stock_ledger()" }, { name: "make_gl_entries()" }] },
        { id: 3102, name: "Delivery Note", path: "doctype/delivery_note/delivery_note.py", nodeType: "code", pos: { x: 850, y: 350 }, icon: "🚚", columns: [{ name: "update_stock_ledger()" }, { name: "make_gl_entries()" }] },
        { id: 3103, name: "Material Request", path: "doctype/material_request/material_request.py", nodeType: "code", pos: { x: 850, y: 650 }, icon: "📝", columns: [{ name: "make_purchase_order()" }, { name: "make_stock_entry()" }] },
        { id: 3104, name: "Pick List", path: "doctype/pick_list/pick_list.py", nodeType: "code", pos: { x: 850, y: 950 }, icon: "📋", columns: [{ name: "set_item_locations()" }, { name: "create_delivery_note()" }] },
        { id: 3105, name: "Landed Cost Voucher", path: "doctype/landed_cost_voucher/landed_cost_voucher.py", nodeType: "code", pos: { x: 850, y: 1250 }, icon: "🚢", columns: [{ name: "update_landed_cost()" }] },
        { id: 3106, name: "Quality Inspection", path: "doctype/quality_inspection/quality_inspection.py", nodeType: "code", pos: { x: 850, y: 1550 }, icon: "🔬", columns: [{ name: "inspect_and_set_status()" }] },
        
        // Data Schemas
        { id: 3201, name: "Stock Entry Schema", path: "doctype/stock_entry/stock_entry.json", nodeType: "db", pos: { x: 1250, y: 50 }, icon: "📄", columns: [{ name: "purpose" }, { name: "items (Table)" }] },
        { id: 3202, name: "Delivery Note Schema", path: "doctype/delivery_note/delivery_note.json", nodeType: "db", pos: { x: 1250, y: 350 }, icon: "📄", columns: [{ name: "customer" }, { name: "items (Table)" }] },
        { id: 3203, name: "Material Request Schema", path: "doctype/material_request/material_request.json", nodeType: "db", pos: { x: 1250, y: 650 }, icon: "📄", columns: [{ name: "material_request_type" }] },
        { id: 3204, name: "Pick List Schema", path: "doctype/pick_list/pick_list.json", nodeType: "db", pos: { x: 1250, y: 950 }, icon: "📄", columns: [{ name: "purpose" }, { name: "locations (Table)" }] },
        { id: 3205, name: "Warehouse Schema", path: "doctype/warehouse/warehouse.json", nodeType: "db", pos: { x: 1250, y: 1850 }, icon: "🏠", columns: [{ name: "is_group" }, { name: "account" }] },
        { id: 3206, name: "Batch Schema", path: "doctype/batch/batch.json", nodeType: "db", pos: { x: 1650, y: 650 }, icon: "📦" },
        { id: 3207, name: "Serial No Schema", path: "doctype/serial_no/serial_no.json", nodeType: "db", pos: { x: 1650, y: 950 }, icon: "🔩" },
        { id: 3208, name: "Serial/Batch Bundle Schema", path: "doctype/serial_and_batch_bundle/serial_and_batch_bundle.json", nodeType: "db", pos: { x: 1650, y: 350 }, icon: "📦" },
        { id: 3209, name: "Stock Closing Balance Schema", path: "doctype/stock_closing_balance/stock_closing_balance.json", nodeType: "db", pos: { x: 1650, y: 50 }, icon: "🧾" },

        // UI & Dashboards
        { id: 3301, name: "Stock Workspace", path: "workspace/stock/stock.json", nodeType: "ui", pos: { x: 50, y: 1250 }, icon: "🏭", columns: [{ name: "Shortcuts" }, { name: "Reports" }] },
        { id: 3302, name: "Stock Balance Page", path: "page/stock_balance/stock_balance.js", nodeType: "ui", pos: { x: 50, y: 1550 }, icon: "📊", columns: [{ name: "Item Dashboard" }] },
        { id: 3303, name: "Item Dashboard", path: "dashboard/item_dashboard.js", nodeType: "ui", pos: { x: 50, y: 1850 }, icon: "📈", columns: [{ name: "refresh()" }] },
        { id: 3304, name: "Stock Entry UI", path: "doctype/stock_entry/stock_entry.js", nodeType: "ui", pos: { x: 2050, y: 50 }, icon: "💻" },
        { id: 3305, name: "Delivery Note UI", path: "doctype/delivery_note/delivery_note.js", nodeType: "ui", pos: { x: 2050, y: 350 }, icon: "💻" },

        // Services & Docs
        { id: 3401, name: "Stock Ledger Spec", path: "spec/README.md", nodeType: "service", pos: { x: 2450, y: 50 }, icon: "ℹ️", columns: [{ name: "Explains SLE fields" }] },
        { id: 3402, name: "Reposting Spec", path: "spec/reposting.md", nodeType: "service", pos: { x: 2450, y: 350 }, icon: "ℹ️", columns: [{ name: "Explains backdated transactions" }] }
    ],
    relationships: [
        // Core Logic Flow
        { from: { table: "Stock Entry" }, to: { table: "Stock Ledger" } },
        { from: { table: "Delivery Note" }, to: { table: "Stock Ledger" } },
        { from: { table: "Stock Ledger", column: "make_sl_entries()" }, to: { table: "Serial/Batch Bundle Logic" } },
        { from: { table: "Stock Ledger", column: "update_entries_after" }, to: { table: "Valuation Logic" } },
        { from: { table: "Auto Reorder Logic" }, to: { table: "Material Request" } },
        { from: { table: "Stock Balance" }, to: { table: "Stock Ledger" } },
        
        // Transactional Flow
        { from: { table: "Pick List" }, to: { table: "Delivery Note" } },
        { from: { table: "Material Request" }, to: { table: "Stock Entry" } },
        { from: { table: "Landed Cost Voucher" }, to: { table: "Stock Ledger" } },
        { from: { table: "Quality Inspection" }, to: { table: "Stock Entry" } },
        
        // MVC Connections
        { from: { table: "Stock Entry UI" }, to: { table: "Stock Entry" } },
        { from: { table: "Stock Entry" }, to: { table: "Stock Entry Schema" }, type: "read" },
        { from: { table: "Delivery Note UI" }, to: { table: "Delivery Note" } },
        { from: { table: "Delivery Note" }, to: { table: "Delivery Note Schema" }, type: "read" },
        { from: { table: "Serial/Batch Bundle Logic" }, to: { table: "Serial/Batch Bundle Schema" }, type: "write" },
        { from: { table: "Serial/Batch Bundle Logic" }, to: { table: "Serial No Schema" }, type: "write" },
        { from: { table: "Serial/Batch Bundle Logic" }, to: { table: "Batch Schema" }, type: "write" },

        // UI Connections
        { from: { table: "Stock Workspace" }, to: { table: "Stock Balance Page" } },
        { from: { table: "Stock Balance Page" }, to: { table: "Item Dashboard" } },
        { from: { table: "Item Dashboard" }, to: { table: "Stock Balance" } }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_19_589699tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Final Chunk
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Controllers
        { id: 2501, name: "AccountsController", path: "controllers/accounts_controller.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "🧾" },
        { id: 2502, name: "StockController", path: "controllers/stock_controller.py", nodeType: "code", pos: { x: 50, y: 300 }, icon: "📦" },
        { id: 2503, name: "SellingController", path: "controllers/selling_controller.py", nodeType: "code", pos: { x: 50, y: 550 }, icon: "📈" },
        { id: 2504, name: "BuyingController", path: "controllers/buying_controller.py", nodeType: "code", pos: { x: 50, y: 800 }, icon: "📉" },
        { id: 2505, name: "SubcontractingController", path: "controllers/subcontracting_controller.py", nodeType: "code", pos: { x: 50, y: 1050 }, icon: "🏭" },
        
        // Stock Module Core Logic
        { id: 3501, name: "Stock Ledger Logic", path: "stock/stock_ledger.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "📚", columns: [{ name: "make_sl_entries()" }, { name: "repost_future_sle()" }] },
        { id: 3502, name: "Stock Balance Logic", path: "stock/stock_balance.py", nodeType: "code", pos: { x: 450, y: 300 }, icon: "⚖️", columns: [{ name: "repost_stock()" }, { name: "get_reserved_qty()" }] },
        { id: 3503, name: "Valuation Logic", path: "stock/valuation.py", nodeType: "code", pos: { x: 450, y: 550 }, icon: "💲", columns: [{ name: "FIFOValuation" }, { name: "LIFOValuation" }] },
        { id: 3504, name: "Serial/Batch Bundle Logic", path: "stock/serial_batch_bundle.py", nodeType: "code", pos: { x: 450, y: 800 }, icon: "📦", columns: [{ name: "SerialBatchBundle" }, { name: "SerialBatchCreation" }] },

        // Stock Transactions
        { id: 3601, name: "Stock Entry Logic", path: "doctype/stock_entry/stock_entry.py", nodeType: "code", pos: { x: 850, y: 100 }, icon: "➡️", columns: [{ name: "update_stock_ledger()" }] },
        { id: 3602, name: "Delivery Note Logic", path: "doctype/delivery_note/delivery_note.py", nodeType: "code", pos: { x: 850, y: 350 }, icon: "🚚", columns: [{ name: "update_stock_ledger()" }] },
        { id: 3603, name: "Purchase Receipt Logic", path: "doctype/purchase_receipt/purchase_receipt.py", nodeType: "code", pos: { x: 850, y: 600 }, icon: "🛒", columns: [{ name: "update_stock_ledger()" }] },
        { id: 3604, name: "Subcontracting Receipt Logic", path: "subcontracting/doctype/subcontracting_receipt/subcontracting_receipt.py", nodeType: "code", pos: { x: 850, y: 850 }, icon: "🏭", columns: [{ name: "update_stock_ledger()" }] },
        { id: 3605, name: "Stock Reconciliation Logic", path: "doctype/stock_reconciliation/stock_reconciliation.py", nodeType: "code", pos: { x: 850, y: 1100 }, icon: "🔄", columns: [{ name: "update_stock_ledger()" }] },
        
        // Stock Schemas
        { id: 3701, name: "Item Schema", path: "doctype/item/item.json", nodeType: "db", pos: { x: 1250, y: 50 }, icon: "📝", columns: [{ name: "has_serial_no" }, { name: "has_batch_no" }] },
        { id: 3702, name: "Stock Ledger Entry Schema", path: "doctype/stock_ledger_entry/stock_ledger_entry.json", nodeType: "db", pos: { x: 1650, y: 50 }, icon: "🧾" },
        { id: 3703, name: "Warehouse Schema", path: "doctype/warehouse/warehouse.json", nodeType: "db", pos: { x: 1250, y: 350 }, icon: "🏠" },
        { id: 3704, name: "Bin Schema", path: "doctype/bin/bin.json", nodeType: "db", pos: { x: 1650, y: 350 }, icon: "📦" },
        { id: 3705, name: "Serial No Schema", path: "doctype/serial_no/serial_no.json", nodeType: "db", pos: { x: 1250, y: 600 }, icon: "🔩" },
        { id: 3706, name: "Batch Schema", path: "doctype/batch/batch.json", nodeType: "db", pos: { x: 1650, y: 600 }, icon: "📦" },
        
        // Stock Reports
        { id: 3801, name: "Stock Balance Report", path: "report/stock_balance/stock_balance.py", nodeType: "ui", pos: { x: 2050, y: 100 }, icon: "📊" },
        { id: 3802, name: "Stock Ledger Report", path: "report/stock_ledger/stock_ledger.py", nodeType: "ui", pos: { x: 2050, y: 350 }, icon: "📊" },
        { id: 3803, name: "Stock Ageing Report", path: "report/stock_ageing/stock_ageing.py", nodeType: "ui", pos: { x: 2050, y: 600 }, icon: "📊" },
        { id: 3804, name: "Repost Item Valuation Tool", path: "doctype/repost_item_valuation/repost_item_valuation.py", nodeType: "service", pos: { x: 2050, y: 850 }, icon: "🔁" }
    ],
    relationships: [
        // Controller Inheritance
        { from: { table: "StockController" }, to: { table: "AccountsController" } },
        { from: { table: "SellingController" }, to: { table: "StockController" } },
        { from: { table: "BuyingController" }, to: { table: "StockController" } },
        { from: { table: "SubcontractingController" }, to: { table: "BuyingController" } },
        
        // Transaction -> Controller -> SLE
        { from: { table: "Stock Entry Logic" }, to: { table: "StockController" } },
        { from: { table: "StockController", column: "update_stock_ledger()" }, to: { table: "Stock Ledger Logic" } },
        { from: { table: "Stock Ledger Logic", column: "make_sl_entries()" }, to: { table: "Stock Ledger Entry Schema" }, type: "write" },
        { from: { table: "Stock Ledger Logic" }, to: { table: "Valuation Logic" } },
        { from: { table: "Stock Ledger Logic" }, to: { table: "Serial/Batch Bundle Logic" } },
        { from: { table: "Delivery Note Logic" }, to: { table: "SellingController" } },
        { from: { table: "Purchase Receipt Logic" }, to: { table: "BuyingController" } },
        { from: { table: "Subcontracting Receipt Logic" }, to: { table: "SubcontractingController" } },
        { from: { table: "Stock Reconciliation Logic" }, to: { table: "StockController" } },
        
        // Schemas
        { from: { table: "Stock Ledger Entry Schema" }, to: { table: "Item Schema" }, type: "read" },
        { from: { table: "Stock Ledger Entry Schema" }, to: { table: "Warehouse Schema" }, type: "read" },
        { from: { table: "Bin Schema" }, to: { table: "Item Schema" }, type: "read" },
        { from: { table: "Bin Schema" }, to: { table: "Warehouse Schema" }, type: "read" },
        { from: { table: "Serial/Batch Bundle Logic" }, to: { table: "Serial No Schema" }, type: "write" },
        { from: { table: "Serial/Batch Bundle Logic" }, to: { table: "Batch Schema" }, type: "write" },

        // Reports
        { from: { table: "Stock Balance Report" }, to: { table: "Bin Schema" }, type: "read" },
        { from: { table: "Stock Ledger Report" }, to: { table: "Stock Ledger Entry Schema" }, type: "read" },
        { from: { table: "Stock Ageing Report" }, to: { table: "Stock Ledger Entry Schema" }, type: "read" },
        { from: { table: "Repost Item Valuation Tool" }, to: { table: "Stock Ledger Logic", column: "repost_future_sle()" } }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>
C:\Users\EmulatorPC\Desktop\biancas\db-designer-00-erpNext-erpnext_chunk_20_582886tokens.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>ERPNext Architecture Analysis - Final Chunk</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>ERPNext - Architecture Analysis</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI/Frontend</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Backend Logic</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Config/Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">ERPNext Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  ERPNext Schema - Final Chunk
//
// ===================================================================================
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        // Core Controllers
        { id: 2502, name: "Stock Controller", path: "controllers/stock_controller.py", nodeType: "code", pos: { x: 50, y: 50 }, icon: "📦", columns: [{ name: "update_stock_ledger()" }, { name: "make_gl_entries()" }] },
        { id: 2503, name: "Selling Controller", path: "controllers/selling_controller.py", nodeType: "code", pos: { x: 50, y: 300 }, icon: "📈", columns: [{ name: "inherits StockController" }] },
        { id: 2504, name: "Buying Controller", path: "controllers/buying_controller.py", nodeType: "code", pos: { x: 50, y: 550 }, icon: "📉", columns: [{ name: "inherits StockController" }] },
        { id: 2505, name: "Subcontracting Controller", path: "controllers/subcontracting_controller.py", nodeType: "code", pos: { x: 50, y: 800 }, icon: "🏭", columns: [{ name: "inherits BuyingController" }] },

        // Stock Module
        { id: 3501, name: "Stock Ledger Logic", path: "stock/stock_ledger.py", nodeType: "code", pos: { x: 450, y: 50 }, icon: "📚", columns: [{ name: "make_sl_entries()" }, { name: "repost_future_sle()" }] },
        { id: 3601, name: "Stock Entry", path: "doctype/stock_entry/stock_entry.py", nodeType: "code", pos: { x: 850, y: 150 }, icon: "➡️", columns: [{ name: "update_stock_ledger()" }, { name: "purpose: Material Transfer/Receipt..." }] },
        { id: 3602, name: "Delivery Note", path: "doctype/delivery_note/delivery_note.py", nodeType: "code", pos: { x: 850, y: 400 }, icon: "🚚", columns: [{ name: "update_stock_ledger()" }] },
        { id: 3603, name: "Purchase Receipt", path: "doctype/purchase_receipt/purchase_receipt.py", nodeType: "code", pos: { x: 850, y: 650 }, icon: "🛒", columns: [{ name: "update_stock_ledger()" }] },

        // Selling & Buying
        { id: 2703, name: "Purchase Order", path: "buying/doctype/purchase_order/purchase_order.py", nodeType: "code", pos: { x: 450, y: 1100 }, icon: "🛒", columns: [{ name: "make_purchase_receipt()" }] },
        { id: 107, name: "Sales Order", path: "selling/doctype/sales_order/sales_order.py", nodeType: "code", pos: { x: 850, y: 1100 }, icon: "📈", columns: [{ name: "make_delivery_note()" }, { name: "make_sales_invoice()" }] },
        { id: 201, name: "Sales Invoice", path: "accounts/doctype/sales_invoice/sales_invoice.py", nodeType: "code", pos: { x: 1250, y: 1100 }, icon: "🧾" },

        // Subcontracting
        { id: 110, name: "Subcontracting Order", path: "subcontracting/doctype/subcontracting_order/subcontracting_order.py", nodeType: "code", pos: { x: 450, y: 1400 }, icon: "🏭", columns: [{ name: "make_subcontracting_receipt()" }] },
        { id: 111, name: "Subcontracting Receipt", path: "subcontracting/doctype/subcontracting_receipt/subcontracting_receipt.py", nodeType: "code", pos: { x: 850, y: 1400 }, icon: "🧾", columns: [{ name: "update_stock_ledger()" }] },
        { id: 112, name: "Subcontracting Inward Order", path: "subcontracting/doctype/subcontracting_inward_order/subcontracting_inward_order.py", nodeType: "code", pos: { x: 1250, y: 1400 }, icon: "🏭", columns: [{ name: "make_work_order()" }] },

        // Quality & Manufacturing
        { id: 1702, name: "Work Order", path: "manufacturing/doctype/work_order/work_order.py", nodeType: "code", pos: { x: 1650, y: 1400 }, icon: "🏗️", columns: [{ name: "create_job_card()" }] },
        { id: 3106, name: "Quality Inspection", path: "quality_management/doctype/quality_inspection/quality_inspection.py", nodeType: "code", pos: { x: 1650, y: 1100 }, icon: "🔬" },
        
        // POS
        { id: 113, name: "POS Controller", path: "selling/page/point_of_sale/pos_controller.js", nodeType: "ui", pos: { x: 2050, y: 50 }, icon: "🛒", columns: [{ name: "prepare_app_defaults()" }, { name: "make_new_invoice()" }] },
        { id: 114, name: "POS Profile", path: "accounts/doctype/pos_profile/pos_profile.py", nodeType: "db", pos: { x: 2450, y: 50 }, icon: "⚙️", columns: [{ name: "warehouse" }, { name: "customer_groups" }] },
        { id: 115, name: "POS Invoice", path: "accounts/doctype/pos_invoice/pos_invoice.py", nodeType: "code", pos: { x: 2050, y: 350 }, icon: "🧾" }
    ],
    relationships: [
        // Controller Inheritance
        { from: { table: "Selling Controller" }, to: { table: "Stock Controller" } },
        { from: { table: "Buying Controller" }, to: { table: "Stock Controller" } },
        { from: { table: "Subcontracting Controller" }, to: { table: "Buying Controller" } },

        // Core Stock Flow
        { from: { table: "Stock Controller" }, to: { table: "Stock Ledger Logic" }, type: "flow" },
        { from: { table: "Stock Entry" }, to: { table: "Stock Controller" }, type: "flow" },
        { from: { table: "Delivery Note" }, to: { table: "Selling Controller" }, type: "flow" },
        { from: { table: "Purchase Receipt" }, to: { table: "Buying Controller" }, type: "flow" },
        { from: { table: "Stock Ledger Logic" }, to: { table: "Bin Schema", name: "(Not in chunk)" }, type: "write" },

        // Sales & Purchase Flow
        { from: { table: "Sales Order" }, to: { table: "Delivery Note" }, type: "write" },
        { from: { table: "Sales Order" }, to: { table: "Sales Invoice" }, type: "write" },
        { from: { table: "Purchase Order" }, to: { table: "Purchase Receipt" }, type: "write" },
        { from: { table: "Purchase Order" }, to: { table: "Quality Inspection" }, type: "flow" },
        { from: { table: "Delivery Note" }, to: { table: "Quality Inspection" }, type: "flow" },
        
        // Subcontracting Flow
        { from: { table: "Purchase Order" }, to: { table: "Subcontracting Order" }, type: "write" },
        { from: { table: "Subcontracting Order" }, to: { table: "Subcontracting Receipt" }, type: "write" },
        { from: { table: "Subcontracting Receipt" }, to: { table: "Subcontracting Controller" }, type: "flow" },
        { from: { table: "Sales Order" }, to: { table: "Subcontracting Inward Order" }, type: "write" },
        { from: { table: "Subcontracting Inward Order" }, to: { table: "Work Order" }, type: "write" },
        { from: { table: "Work Order" }, to: { table: "Stock Entry" }, type: "write" },
        
        // POS Flow
        { from: { table: "POS Controller" }, to: { table: "POS Profile" }, type: "read" },
        { from: { table: "POS Controller" }, to: { table: "POS Invoice" }, type: "write" },
        { from: { table: "POS Invoice" }, to: { table: "Sales Invoice" }, type: "flow" }
    ]
};



// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${table.name}${pathSpan}`;

            const list = document.createElement('ul');
            list.innerHTML = (table.columns || []).map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : (col.type || '');
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromTableName = typeof rel.from === 'string' ? rel.from : rel.from.table;
            const toTableName = typeof rel.to === 'string' ? rel.to : rel.to.table;

            const fromId = idMap.get(fromTableName);
            const toId = idMap.get(toTableName);
            if(!fromId || !toId) return;

            let fromColName = (typeof rel.from === 'object' && rel.from.column) ? (typeof rel.from.column === 'string' ? rel.from.column : (rel.from.column.name || '')) : '';
            let toColName = (typeof rel.to === 'object' && rel.to.column) ? (typeof rel.to.column === 'string' ? rel.to.column : (rel.to.column.name || '')) : '';
            
            let fromElId = fromColName ? `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${fromId}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = toColName ? `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}` : `${canvasId}-${toId}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            const type = rel.type || 'read';

            if (type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }
    
    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>


i leave you here a old example just for you as reference on what kind of output i exect from you:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Raptor 3: OpenRA Master Architecture</title>
<style>
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background-color: #111827; color: #d1d5db; margin: 0; display: flex; flex-direction: column; height: 100vh; overflow: hidden; }
    .header { background-color: #1f2937; padding: 1rem 2rem; border-bottom: 1px solid #374151; flex-shrink: 0; display: flex; justify-content: space-between; align-items: center; }
    h1 { color: white; margin: 0; }
    .controls { display: flex; align-items: center; gap: 20px; }
    .legend { display: flex; gap: 20px; font-size: 12px; align-items: center; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .main-container { display: flex; flex-grow: 1; }
    .panel { min-width: 150px; height: 100%; display: flex; flex-direction: column; position: relative; }
    .panel:nth-child(1) { flex: 0 1 15%; }
    .panel:nth-child(3) { flex: 1 1 70%; }
    .panel:nth-child(5) { flex: 0 1 15%; }

    .splitter { width: 6px; background-color: #374151; cursor: col-resize; flex-shrink: 0; z-index: 100; }
    .splitter:hover { background-color: #4b5563; }
    .panel-header { padding: 1rem; text-align: center; border-bottom: 1px solid #374151; background-color: #1f2937; }
    .panel-header h2 { margin: 0; font-size: 1.5rem; }
    .header-r2 { color: #fca5a5; }
    .header-r3 { color: #86efac; }
    .header-r4 { color: #c4b5fd; }
    .canvas { position: relative; width: 100%; flex-grow: 1; overflow: hidden; cursor: grab; }
    .canvas:active { cursor: grabbing; }
    .connections { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
    .transform-container { position: absolute; top: 0; left: 0; transform-origin: 0 0; z-index: 2; }
    
    .node { position: absolute; border: 3px solid #4b5563; border-radius: 8px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3); font-family: monospace; width: 280px; cursor: move; z-index: 10; user-select: none; padding-top: 30px; }
    .node h3 { padding: 8px 12px 8px 12px; margin: 0; border-bottom: 1px solid rgba(0,0,0,0.2); border-radius: 8px 8px 0 0; font-size: 14px; color: white; word-break: break-all; }
    .node h3 .path { font-size: 0.8em; color: #9ca3af; display: block; font-weight: normal; }
    .node ul { list-style: none; padding: 0; margin: 0; }
    .node li { display: flex; align-items: center; padding: 8px 12px; border-bottom: 1px solid rgba(255,255,255,0.05); font-size: 12px; position: relative; }
    .node li:last-child { border-bottom: none; }
    .node .col-name { font-weight: 500; }
    .node .col-type { margin-left: auto; color: #9ca3af; }

    .db-node { background-color: rgba(196, 181, 253, 0.15); border-color: #a78bfa; }
    .db-node h3 { background-color: #8b5cf6; }
    
    .ui-node { background-color: rgba(191, 219, 254, 0.15); border-color: #60a5fa; }
    .ui-node h3 { background-color: #3b82f6; }

    .code-node { background-color: rgba(134, 239, 172, 0.1); border-color: #4ade80; }
    .code-node h3 { background-color: #22c55e; }

    .service-node { background-color: rgba(252, 165, 165, 0.1); border-color: #f87171; }
    .service-node h3 { background-color: #ef4444; }
    
    .icon-display { position: absolute; top: -32px; left: 50%; transform: translateX(-50%); font-size: 64px; z-index: 12; pointer-events: none; opacity: 0.8; }
</style>
</head>
<body>

<div class="header">
    <h1>Full Stack Designer - OpenRA Master Architecture</h1>
    <div class="controls">
        <div class="legend">
             <div class="legend-item"><svg width="10" height="10" style="background:#3b82f6; border-radius:3px;"></svg> UI</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#22c55e; border-radius:3px;"></svg> Code</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#8b5cf6; border-radius:3px;"></svg> Data/Schema</div>
            <div class="legend-item"><svg width="10" height="10" style="background:#ef4444; border-radius:3px;"></svg> Service</div>
        </div>
    </div>
</div>

<div class="main-container">
    <div class="panel">
        <div class="panel-header"><h2 class="header-r2">Raptor 2: Legacy</h2></div>
        <div id="canvas-r2" class="canvas"><svg id="connections-r2" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r3">OpenRA Engine</h2></div>
        <div id="canvas-r3" class="canvas"><svg id="connections-r3" class="connections"></svg><div class="transform-container"></div></div>
    </div>
    <div class="splitter"></div>
    <div class="panel">
        <div class="panel-header"><h2 class="header-r4">Raptor 4: Future</h2></div>
        <div id="canvas-r4" class="canvas"><svg id="connections-r4" class="connections"></svg><div class="transform-container"></div></div>
    </div>
</div>

<script>
// ===================================================================================
//
//  MASTER DATA SOURCES
//
// ===================================================================================
/*
    ARCHITECTURAL INSIGHTS FOR FUTURE AI ANALYSIS:
    This file visualizes the comprehensive architecture of the OpenRA engine. The design is highly data-driven, following an entity-component-system (Actor-Trait-Activity) pattern where C# code provides core functionality, but game content (units, rules, missions, assets) is defined in external data files.

    **Overall Architectural Philosophy:**
    The engine separates core logic (C#) from game content and rules (YAML, Lua). This allows for extensive modding without altering the engine's source code. The "database schema" is not a single SQL file but is defined implicitly through C# classes (`*Info.cs`) and populated by human-readable YAML files. This separation is the key to the engine's flexibility and is demonstrated by the intelligent aggregation and deduplication of its components. A master architectural diagram reveals a much smaller set of unique components than one would expect, highlighting a high degree of reuse.

    **Intelligent Aggregation and Deduplication:**
    Analysis of the engine's structure across 11 different source files, initially suggesting ~287 architectural nodes, reveals the power of this modular design. Through intelligent deduplication, the final unique node count is only 119. This is not an error, but a core feature of the architecture, where 168 duplicate nodes were identified and merged. This efficiency stems from several areas:
    - **High Degree of Overlap in Core Engine Components:** Core C# classes like `Game.cs`, `World.cs`, `Actor.cs`, and `Ruleset.cs` appear in almost every visualization but are correctly identified as a single, unified entity.
    - **Repetitive Mission Structure:** Mission-specific files (`allies-06b`, `soviet-04a`, etc.) share a common pattern, reusing components like `map.yaml`, `rules.yaml`, and shared Lua scripts (e.g., `campaign.lua`).
    - **Shared Mod-Level Definitions:** Different aspects of the same mod reuse high-level rule files like `defaults.yaml`, `vehicles.yaml`, and `weapons.yaml`, preventing redundancy.
    - **Merging, Not Discarding:** It's crucial to understand that duplicate nodes are not discarded but are merged. For example, if one file defines `Actor.cs` with a `Tick()` method and another defines it with a `ResolveOrder()` method, the final, synthesized `Actor.cs` node contains both, creating a more complete and accurate representation.

    **Key File Types and Their Roles:**
    - C# Classes (Core Engine):
        - `Game.cs`: The main application entry point, responsible for loading mods and maps.
        - `Ruleset.cs`: The master container for all game rules. It parses YAML files to build an in-memory database of all possible actors, weapons, etc., for a given mod.
        - `World.cs`: Represents the live game state, managing all actors and the terrain.
        - `Actor.cs`: The base class for every object in the game (units, buildings, projectiles). It is a container for `Trait`s.
        - `TraitInfo.cs` / `*Info.cs`: C# classes that act as blueprints for traits, defining the data fields that can be set in YAML.
        - `Trait`s (e.g., `Mobile.cs`, `Health.cs`, `Armament.cs`): The actual components that give an `Actor` its behavior and properties.
    - YAML Files (Data/Schema):
        - `mod.yaml`: The manifest for a mod, listing all rules, assets, missions, and other files to be loaded.
        - `rules/*.yaml`: Define the concrete game entities (units, buildings). They use `Inherits:` to build upon abstract templates, creating a powerful data-driven inheritance model.
        - `sequences/*.yaml`: Link game actors to their visual animations and binary sprite files (`.shp`).
        - `map.yaml`: The instance document for a specific level. It defines the initial state of the world, including every actor's type, location, and owner.
    - Lua Script Files (`*.lua`):
        - Contain event-driven mission logic and AI behavior. They interact with the C# engine via Triggers and direct commands, acting as the "business logic" layer for scenarios.
    - Binary Assets (Services):
        - `*.shp`: Raw sprite and animation data.
        - `*.aud`, `*.vqa`: Raw audio and video assets.
        - `*.bin`: Raw, grid-based terrain geometry for a map.

    **The Data Flow Pipeline:**
    1.  **Engine Start:** `Game.cs` loads a mod by reading its `mod.yaml` manifest.
    2.  **Rule Compilation:** `Ruleset.cs` parses all `rules/*.yaml` files specified in the manifest, creating a complete in-memory "database" of all actor and weapon definitions.
    3.  **Map Instantiation:** The engine loads a `map.yaml` file. For each entry in the `Actors:` list, it queries the `Ruleset` for the actor's full definition and creates a live `Actor.cs` instance in the `World.cs`.
    4.  **Gameplay Loop:** Player input is translated into `Order`s, which are handled by `Trait`s on an `Actor`. These traits queue `Activity`s (e.g., 'Move', 'Attack') that execute over time, using other traits and core systems (like the `Pathfinder`) to perform their actions.
    5.  **Asset Linking:** When an `Actor` needs to be rendered, its `Render` traits look up the correct animation in `sequences/*.yaml`, which in turn points to the required binary asset (`.shp` file) to be drawn on screen.
*/
const schemaR2 = { tables: [], relationships: [] };
const schemaR4 = { tables: [], relationships: [] };

const schemaR3 = {
    tables: [
        { id: 1, name: "OpenRA.Launcher", path: "OpenRA.Launcher/Program.cs", nodeType: "ui", pos: { x: 50, y: 50 }, icon: "🚀", columns: [ { name: "Main(string[] args)" }, { name: "Game.InitializeAndRun()" } ] },
        { id: 2, name: "Widget System", path: "OpenRA.Game/Widgets/Widget.cs", nodeType: "ui", pos: { x: 50, y: 350 }, icon: "🖼️", columns: [ { name: "Ui.Tick()" }, { name: "Ui.Draw()" }, { name: "HandleMouseInput()" }, { name: "HandleKeyPress()" } ] },
        { id: 3, name: "WidgetLoader.cs", path: "OpenRA.Game/Widgets/", nodeType: "ui", pos: { x: 50, y: 650 }, icon: "🧩", columns: [ { name: "LoadWidget()" } ] },
        { id: 4, name: "WorldInteractionControllerWidget.cs", path: "Widgets/", nodeType: "ui", pos: { x: 50, y: 950 }, icon: "🖱️", columns: [ { name: "HandleMouseInput()" } ] },
        { id: 5, name: "UnitOrderGenerator.cs", path: "Orders/", nodeType: "ui", pos: { x: 50, y: 1250 }, icon: "📜", columns: [ { name: "Order()" }, { name: "GetCursor()" } ] },
        { id: 6, name: "mainmenu.yaml", path: "mods/cnc/chrome/", nodeType: "ui", pos: { x: 50, y: 1550 }, icon: "🖥️", columns: [ { name: "SINGLEPLAYER_BUTTON" }, { name: "MULTIPLAYER_BUTTON" } ] },
        { id: 7, name: "lobby.yaml", path: "mods/cnc/chrome/", nodeType: "ui", pos: { x: 50, y: 1850 }, icon: "🛋️", columns: [ { name: "START_GAME_BUTTON" }, { name: "MAP_PREVIEW_ROOT" } ] },
        { id: 8, name: "settings.yaml", path: "mods/cnc/chrome/", nodeType: "ui", pos: { x: 50, y: 2150 }, icon: "⚙️", columns: [ { name: "DISPLAY_PANEL" }, { name: "AUDIO_PANEL" }, { name: "HOTKEYS_PANEL" } ] },
        { id: 9, name: "RenderSprites.cs", path: "Traits/Render/", nodeType: "ui", pos: { x: 50, y: 2450 }, icon: "🖼️", columns: [ { name: "Render()" } ] },
        { id: 10, name: "WithSpriteBody.cs", path: "Traits/Render/", nodeType: "ui", pos: { x: 50, y: 2750 }, icon: "🧍", columns: [ { name: "DefaultAnimation" } ] },
        { id: 11, name: "ingame-player.yaml", path: "mods/ra/chrome/", nodeType: "ui", pos: { x: 50, y: 3050 }, icon: "🖥️", columns: [ { name: "@SIDEBAR_PRODUCTION" }, { name: "@COMMAND_BAR" } ] },
        { id: 12, name: "map.ftl", path: "bomber-john/", nodeType: "ui", pos: { x: 50, y: 3350 }, icon: "💬", columns: [ { name: "actor-mnlyr-name = Bomber" }, { name: "actor-minvv.name = Bomb" } ] },
        { id: 13, name: "Game.cs", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 50 }, icon: "🎮", columns: [ { name: "InitializeAndRun()" }, { name: "Loop()" }, { name: "LogicTick()" }, { name: "RenderTick()" }, { name: "LoadMap(mapName)" }, { name: "StartGame()" } ] },
        { id: 14, name: "World.cs", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 350 }, icon: "🌍", columns: [ { name: "Tick()" }, { name: "CreateActor()" }, { name: "SyncHash()" }, { name: "CreateActor(actorInfo)" }, { name: "LoadTerrain(mapData)" } ] },
        { id: 15, name: "Actor.cs", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 650 }, icon: "🤖", columns: [ { name: "Tick()" }, { name: "ResolveOrder()" }, { name: "TraitsImplementing<T>()" }, { name: "LoadPassenger()" }, { name: "Destroy()" }, { name: "IsDead" }, { name: "Owner" }, { name: "Location" }, { name: "Move()" }, { name: "AttackMove()" }, { name: "Build()" }, { name: "Demolish()" }, { name: "Infiltrate()" }, { name: "Health" }, { name: "TransformsInto" }, { name: "FireWarheadsOnDeath" }, { name: "Produce(unit)" }, { name: "GrantCondition('unkillable')" }, { name: "Capture()" }, { name: "Sell()" }, { name: "ActivateNukePower()" }, { name: "Info (ActorInfo)" } ] },
        { id: 16, name: "Player.cs", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 950 }, icon: "🧑", columns: [ { name: "PlayerName" }, { name: "Faction" }, { name: "RelationshipWith()" } ] },
        { id: 17, name: "OrderManager.cs", path: "OpenRA.Game/Network/", nodeType: "code", pos: { x: 450, y: 1250 }, icon: "📦", columns: [ { name: "IssueOrder()" }, { name: "ReceiveOrders()" }, { name: "TryTick()" } ] },
        { id: 18, name: "WorldRenderer.cs", path: "OpenRA.Game/Graphics/", nodeType: "code", pos: { x: 450, y: 1550 }, icon: "🎨", columns: [ { name: "PrepareRenderables()" }, { name: "Draw()" }, { name: "ScreenPxPosition()" } ] },
        { id: 19, name: "TraitDictionary.cs", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 1850 }, icon: "📚", columns: [ { name: "AddTrait()" }, { name: "Get<T>()" }, { name: "ActorsWithTrait<T>()" } ] },
        { id: 20, name: "Activity.cs", path: "OpenRA.Game/Activities/", nodeType: "code", pos: { x: 450, y: 2150 }, icon: "🏃", columns: [ { name: "TickOuter()" }, { name: "OnFirstRun()" }, { name: "Cancel()" }, { name: "ScriptedMove()" }, { name: "Wait()" } ] },
        { id: 21, name: "Connection.cs", path: "OpenRA.Game/Network/", nodeType: "code", pos: { x: 450, y: 2450 }, icon: "🔌", columns: [ { name: "Send()" }, { name: "Receive()" } ] },
        { id: 22, name: "Sound.cs", path: "OpenRA.Game/Sound/", nodeType: "code", pos: { x: 450, y: 2750 }, icon: "🔊", columns: [ { name: "Play()" }, { name: "PlayMusic()" } ] },
        { id: 23, name: "Manifest.cs (Mod Definition)", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 3050 }, icon: "📦", columns: [ { name: "Rules" }, { name: "Sequences" }, { name: "Weapons" }, { name: "Chrome" } ] },
        { id: 24, name: "Sandworm.cs (Mod Trait)", path: "OpenRA.Mods.D2k/Traits/", nodeType: "code", pos: { x: 450, y: 3350 }, icon: "🐛", columns: [ { name: "Tick()" }, { name: "RescanForTargets()" } ] },
        { id: 25, name: "AttractsWorms.cs (Mod Trait)", path: "OpenRA.Mods.D2k/Traits/", nodeType: "code", pos: { x: 450, y: 3650 }, icon: "🔊", columns: [ { name: "Intensity" }, { name: "AttractionAtPosition()" } ] },
        { id: 26, name: "campaign.lua", path: "mods/cnc/scripts/", nodeType: "code", pos: { x: 450, y: 3950 }, icon: "📜", columns: [ { name: "InitObjectives()" }, { name: "ReinforceWithLandingCraft()" }, { name: "ProduceUnits()" }, { name: "CheckForBase()" }, { name: "InitObjectives(player)" }, { name: "ReinforceWithTransport(...)" } ] },
        { id: 27, name: "nod09.lua", path: "mods/cnc/maps/nod09/", nodeType: "code", pos: { x: 450, y: 4250 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "SendGDIAirstrike()" }, { name: "CheckForSams()" } ] },
        { id: 28, name: "allies08b.lua", path: "allies-08b/", nodeType: "code", pos: { x: 450, y: 4550 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "Tick() (Timer)" }, { name: "CreateScientists()" }, { name: "DefendChronosphereCompleted()" }, { name: "Trigger.OnAnyKilled(...)" }, { name: "Trigger.OnEnteredFootprint(...)" } ] },
        { id: 29, name: "allies08b-AI.lua", path: "allies-08b/", nodeType: "code", pos: { x: 450, y: 4850 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ProduceInfantry()" }, { name: "ProduceVehicles()" }, { name: "GroundWaves()" }, { name: "WTransWaves()" } ] },
        { id: 30, name: "Game.cs (Engine Entry)", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 5150 }, icon: "🎮", columns: [ { name: "Main()" }, { name: "LoadMod(modId)" }, { name: "LoadMap(mapName)" } ] },
        { id: 31, name: "Ruleset.cs (Data Loader)", path: "OpenRA.Game/GameRules/", nodeType: "code", pos: { x: 450, y: 5450 }, icon: "📚", columns: [ { name: "LoadFromMod()" }, { name: "ActorInfoFor(actorName)" } ] },
        { id: 32, name: "World.cs (Game State)", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 5750 }, icon: "🌍", columns: [ { name: "CreateActor(actorInfo)" }, { name: "Tick()" } ] },
        { id: 33, name: "Actor.cs (Game Object)", path: "OpenRA.Game/", nodeType: "code", pos: { x: 450, y: 6050 }, icon: "🤖", columns: [ { name: "Info (ActorInfo)" }, { name: "Owner" }, { name: "Location" } ] },
        { id: 34, name: "allies05c.lua", path: "allies-05c/", nodeType: "code", pos: { x: 450, y: 6350 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "InitTriggers()" }, { name: "Trigger.OnInfiltrated(Warfactory,..)" }, { name: "Trigger.OnInfiltrated(Prison,..)" }, { name: "WarfactoryInfiltrated()" }, { name: "FreeTanya()" }, { name: "SendReinforcements()" } ] },
        { id: 35, name: "allies05c-AI.lua", path: "allies-05c/", nodeType: "code", pos: { x: 450, y: 6650 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ProduceUSSRInfantry()" }, { name: "ProduceUSSRVehicles()" }, { name: "SendAttackGroup()" } ] },
        { id: 36, name: "allies10a.lua", path: "allies-10a/", nodeType: "code", pos: { x: 450, y: 6950 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "MissionStart()" }, { name: "MissionTriggers()" }, { name: "Trigger.OnEnteredProximityTrigger(...)" }, { name: "LaunchMissiles()" }, { name: "ActivateAI()" } ] },
        { id: 37, name: "allies10a-AI.lua", path: "allies-10a/", nodeType: "code", pos: { x: 450, y: 7250 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ProduceInfantry()" }, { name: "ProduceVehicles()" }, { name: "SendAttackGroup()" }, { name: "Paradrop()" } ] },
        { id: 38, name: "atreides05.lua", path: "atreides-05/", nodeType: "code", pos: { x: 450, y: 7550 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "SendHarkonnen()" }, { name: "SendMercenaries()" }, { name: "Trigger.OnCapture(Starport,...)" }, { name: "Trigger.OnKilled(HarkonnenBarracks,...)" } ] },
        { id: 39, name: "atreides05-AI.lua", path: "atreides-05/", nodeType: "code", pos: { x: 450, y: 7850 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ProduceInfantry()" }, { name: "SendAttack()" } ] },
        { id: 40, name: "harkonnen09a.lua", path: "harkonnen-09a/", nodeType: "code", pos: { x: 450, y: 8150 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "Trigger.AfterDelay(...)" }, { name: "SendAirStrike()" }, { name: "BuildFremen()" }, { name: "SendHarkonnenReinforcements()" }, { name: "ActivateAI()" } ] },
        { id: 41, name: "harkonnen09a-AI.lua", path: "harkonnen-09a/", nodeType: "code", pos: { x: 450, y: 8450 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "DefendAndRepairBase(...)" }, { name: "ProduceUnits(AtreidesMain, ...)" }, { name: "ProduceUnits(CorrinoMain, ...)" } ] },
        { id: 42, name: "ordos05.lua", path: "ordos-05/", nodeType: "code", pos: { x: 450, y: 8750 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "Tick()" }, { name: "Trigger.OnCapture(AStarport,...)" }, { name: "Trigger.OnKilled(AStarport,...)" }, { name: "ActivateAI()" } ] },
        { id: 43, name: "ordos05-AI.lua", path: "ordos-05/", nodeType: "code", pos: { x: 450, y: 9050 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ActivateAIProduction()" }, { name: "ProduceUnits(AtreidesMain,...)" }, { name: "DefendAndRepairBase(...)" } ] },
        { id: 44, name: "allies06b.lua", path: "allies-06b/", nodeType: "code", pos: { x: 450, y: 9350 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "InfiltrateTechCenter()" }, { name: "Trigger.OnInfiltrated(a, ...)" }, { name: "Trigger.OnCapture(RadarDome, ...)" }, { name: "ActivateAI()" } ] },
        { id: 45, name: "allies06b-AI.lua", path: "allies-06b/", nodeType: "code", pos: { x: 450, y: 9650 }, icon: "🧠", columns: [ { name: "ActivateAI()" }, { name: "ProduceInfantry()" }, { name: "ProduceVehicles()" }, { name: "WTransWaves()" }, { name: "SendAttack(units, path)" } ] },
        { id: 46, name: "soviet04a.lua", path: "soviet-04a/", nodeType: "code", pos: { x: 450, y: 9950 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "RunInitialActivities()" }, { name: "Trigger.OnKilled(RadarDome, ...)" }, { name: "Trigger.OnAllKilled(Village, ...)" } ] },
        { id: 47, name: "soviet04a-AI.lua", path: "soviet-04a/", nodeType: "code", pos: { x: 450, y: 10250 }, icon: "🧠", columns: [ { name: "BuildBase()" }, { name: "ProduceInfantry()" }, { name: "ProduceArmor()" }, { name: "SendUnits(units, waypoints)" } ] },
        { id: 48, name: "soviet04a-reinforcements.lua", path: "soviet-04a/", nodeType: "code", pos: { x: 450, y: 10550 }, icon: "✈️", columns: [ { name: "ReinfInf()" }, { name: "ReinfArmor()" }, { name: "BringPatrol1()" } ] },
        { id: 49, name: "Order.cs", path: "(Core Engine)", nodeType: "code", pos: { x: 450, y: 10850 }, icon: "📦", columns: [ { name: "OrderString" }, { name: "Subject (Actor)" }, { name: "Target" } ] },
        { id: 50, name: "Actor.cs (Core)", path: "(Core Engine)", nodeType: "code", pos: { x: 450, y: 11150 }, icon: "🤖", columns: [ { name: "QueueActivity()" }, { name: "Tick() -> Tick activities" }, { name: "TraitsImplementing<T>()" } ] },
        { id: 51, name: "Move.cs (Activity)", path: "Activities/Move/", nodeType: "code", pos: { x: 450, y: 11450 }, icon: "🏃", columns: [ { name: "Tick()" }, { name: "Uses -> IMove" } ] },
        { id: 52, name: "Attack.cs (Activity)", path: "Activities/", nodeType: "code", pos: { x: 450, y: 11750 }, icon: "💥", columns: [ { name: "Tick()" }, { name: "Uses -> AttackBase" } ] },
        { id: 53, name: "Mobile.cs (IResolveOrder)", path: "Traits/", nodeType: "code", pos: { x: 450, y: 12050 }, icon: "➡️", columns: [ { name: "ResolveOrder('Move')" }, { name: "PathFinder.FindPath()" } ] },
        { id: 54, name: "AttackFollow.cs (IResolveOrder)", path: "Traits/Attack/", nodeType: "code", pos: { x: 450, y: 12350 }, icon: "🎯", columns: [ { name: "ResolveOrder('Attack')" }, { name: "DoAttack()" } ] },
        { id: 55, name: "Armament.cs", path: "Traits/", nodeType: "code", pos: { x: 450, y: 12650 }, icon: "🔫", columns: [ { name: "CheckFire()" }, { name: "WeaponInfo" } ] },
        { id: 56, name: "Health.cs", path: "Traits/", nodeType: "code", pos: { x: 450, y: 12950 }, icon: "❤️", columns: [ { name: "InflictDamage()" } ] },
        { id: 57, name: "HierarchicalPathFinder.cs", path: "Pathfinder/", nodeType: "code", pos: { x: 450, y: 13250 }, icon: "🗺️", columns: [ { name: "FindPath()" } ] },
        { id: 58, name: "Live Game World", path: "(In Memory)", nodeType: "code", pos: { x: 450, y: 13550 }, icon: "💡", columns: [ { name: "Rendered Terrain" }, { name: "Actor Instances" }, { name: "Player States" } ] },
        { id: 59, name: "fields-of-green.lua", path: "fields-of-green/", nodeType: "code", pos: { x: 450, y: 13850 }, icon: "📜", columns: [ { name: "WorldLoaded()" }, { name: "SetupFactories()" }, { name: "SetupInvulnerability()" }, { name: "ProduceUnits(factory, units)" }, { name: "SendNodInfantry()" }, { name: "SendGDIVehicles()" }, { name: "BindActorTriggers(actor, loc)" } ] },
        { id: 60, name: "Ruleset.cs", path: "OpenRA.Game/GameRules/", nodeType: "db", pos: { x: 850, y: 50 }, icon: "📜", columns: [ { name: "Actors (Dictionary)" }, { name: "Weapons (Dictionary)" }, { name: "LoadDefaults()" } ] },
        { id: 61, name: "ActorInfo.cs", path: "OpenRA.Game/GameRules/", nodeType: "db", pos: { x: 850, y: 350 }, icon: "📝", columns: [ { name: "Name" }, { name: "TraitsInConstructOrder()" }, { name: "TraitInfo<T>()" } ] },
        { id: 62, name: "TraitInfo.cs", path: "OpenRA.Game/Traits/", nodeType: "db", pos: { x: 850, y: 650 }, icon: "🔧", columns: [ { name: "Create(ActorInitializer)" }, { name: "Requires<T>" }, { name: "NotBefore<T>" } ] },
        { id: 63, name: "Map.cs", path: "OpenRA.Game/Map/", nodeType: "db", pos: { x: 850, y: 950 }, icon: "🗺️", columns: [ { name: "MapSize" }, { name: "Tiles (CellLayer)" }, { name: "Height (CellLayer)" }, { name: "Actors (Definitions)" } ] },
        { id: 64, name: "MiniYaml.cs", path: "OpenRA.Game/", nodeType: "db", pos: { x: 850, y: 1250 }, icon: "📄", columns: [ { name: "FromFile()" }, { name: "FromStream()" }, { name: "Merge()" } ] },
        { id: 65, name: "FieldLoader.cs", path: "OpenRA.Game/", nodeType: "db", pos: { x: 850, y: 1550 }, icon: "📥", columns: [ { name: "Load(object, MiniYaml)" }, { name: "GetValue<T>()" } ] },
        { id: 66, name: "WeaponInfo.cs", path: "OpenRA.Game/GameRules/", nodeType: "db", pos: { x: 850, y: 1850 }, icon: "💥", columns: [ { name: "Range" }, { name: "Projectile" }, { name: "Warheads" } ] },
        { id: 67, name: "Order.cs", path: "OpenRA.Game/Network/", nodeType: "db", pos: { x: 850, y: 2150 }, icon: "➡️", columns: [ { name: "OrderString" }, { name: "Subject" }, { name: "Target" }, { name: "Serialize()" } ] },
        { id: 68, name: "temperat.yaml", path: "mods/cnc/tilesets/", nodeType: "db", pos: { x: 850, y: 2450 }, icon: "🏞️", columns: [ { name: "General (Tileset Def)" }, { name: "Terrain (Types)" }, { name: "Templates (Tile Rules)" }, { name: "MultiBrushCollections" } ] },
        { id: 69, name: "ai.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 2750 }, icon: "🧠", columns: [ { name: "ModularBot Definitions" }, { name: "SupportPowerBotModule" }, { name: "BaseBuilderBotModule" }, { name: "UnitBuilderBotModule" } ] },
        { id: 70, name: "aircraft.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 3050 }, icon: "✈️", columns: [ { name: "TRAN (Transport)" }, { name: "HELI (Apache)" }, { name: "ORCA (Orca)" }, { name: "C17 (Cargo Plane)" } ] },
        { id: 71, name: "nod09/map.yaml", path: "mods/cnc/maps/", nodeType: "db", pos: { x: 850, y: 3350 }, icon: "🗺️", columns: [ { name: "Title: Reinforce Egypt" }, { name: "Tileset: DESERT" }, { name: "Players: GDI, Nod" }, { name: "Actors: ..." }, { name: "Rules: nod09.lua" } ] },
        { id: 72, name: "world.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 3650 }, icon: "📜", columns: [ { name: "Locomotor@FOOT" }, { name: "Locomotor@WHEELED" } ] },
        { id: 73, name: "player.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 3950 }, icon: "🧑‍⚖️", columns: [ { name: "^BasePlayer" }, { name: "SupportPowerManager" } ] },
        { id: 74, name: "infantry.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 4250 }, icon: "🚶", columns: [ { name: "E1: ^Soldier" }, { name: "Cost: 100" }, { name: "Weapon: M16" } ] },
        { id: 75, name: "vehicles.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 4550 }, icon: "🚚", columns: [ { name: "MCV: ^Vehicle" }, { name: "Transforms: IntoActor: fact" } ] },
        { id: 76, name: "structures.yaml", path: "mods/cnc/rules/", nodeType: "db", pos: { x: 850, y: 4850 }, icon: "🏗️", columns: [ { name: "FACT: ^BaseBuilding" }, { name: "Production:" }, { name: "Power:" } ] },
        { id: 77, name: "infantry.yaml (Sequences)", path: "mods/cnc/sequences/", nodeType: "db", pos: { x: 850, y: 5150 }, icon: "🎬", columns: [ { name: "e1:" }, { name: "stand: Facings: 8" }, { name: "run: Length: 6" } ] },
        { id: 78, name: "vehicles.yaml (Sequences)", path: "mods/cnc/sequences/", nodeType: "db", pos: { x: 850, y: 5450 }, icon: "🎬", columns: [ { name: "mcv:" }, { name: "idle: Facings: 32" } ] },
        { id: 79, name: "map.yaml", path: "allies-08b/", nodeType: "db", pos: { x: 850, y: 5750 }, icon: "🗺️", columns: [ { name: "Title: Protect the Chronosphere" }, { name: "Players: Greece, USSR, England" }, { name: "Chronosphere: pdox" }, { name: "USSRWarFactory: weap" }, { name: "AttackChrono: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 80, name: "rules.yaml", path: "allies-08b/", nodeType: "db", pos: { x: 850, y: 6050 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: allies08b.lua" }, { name: "           allies08b-AI.lua" }, { name: "MissionData: BriefingVideo: ally8.vqa" }, { name: "MCV: Buildable: ~disabled" } ] },
        { id: 81, name: "mod.yaml (Mod Manifest)", path: "mods/ts/mod.yaml", nodeType: "db", pos: { x: 850, y: 6350 }, icon: "📦", columns: [ { name: "Title: Tiberian Sun" }, { name: "Rules: [...]" }, { name: "Sequences: [...]" }, { name: "Weapons: [...]" }, { name: "Missions: missions.yaml" } ] },
        { id: 82, name: "missions.yaml (Mission List)", path: "mods/ra/missions.yaml", nodeType: "db", pos: { x: 850, y: 6650 }, icon: "📄", columns: [ { name: "Allied Campaign:" }, { name: "  allies-01" }, { name: "Soviet Campaign:" }, { name: "  soviet-01" } ] },
        { id: 83, name: "map.yaml (Level Instance)", path: "maps/sunstroke/map.yaml", nodeType: "db", pos: { x: 850, y: 6950 }, icon: "🗺️", columns: [ { name: "RequiresMod: ts" }, { name: "Tileset: TEMPERATE" }, { name: "Actors:" }, { name: "  Actor615: mpspawn" }, { name: "  Actor627: trock05" } ] },
        { id: 84, name: "defaults.yaml (Base Types)", path: "mods/ts/rules/", nodeType: "db", pos: { x: 850, y: 7250 }, icon: "📜", columns: [ { name: "^Infantry" }, { name: "^Vehicle" }, { name: "^Building" } ] },
        { id: 85, name: "vehicles.yaml (Concrete Types)", path: "mods/ts/rules/", nodeType: "db", pos: { x: 850, y: 7550 }, icon: "🚚", columns: [ { name: "4TNK (Mammoth Tank)" }, { name: "Inherits: ^Vehicle" }, { name: "Armament: Weapon: 120mm" }] },
        { id: 86, name: "weapons.yaml (Component Data)", path: "mods/ts/weapons/", nodeType: "db", pos: { x: 850, y: 7850 }, icon: "💥", columns: [ { name: "120mm:" }, { name: "ReloadDelay: 80" }, { name: "Range: 6c768" } ] },
        { id: 87, name: "sequences/vehicles.yaml", path: "mods/ts/sequences/", nodeType: "db", pos: { x: 850, y: 8150 }, icon: "🎬", columns: [ { name: "4tnk:" }, { name: "  idle: ..." }, { name: "  Filename: 4tnk.shp" } ] },
        { id: 88, name: "map.yaml", path: "allies-05c/", nodeType: "db", pos: { x: 850, y: 8450 }, icon: "🗺️", columns: [ { name: "Title: Tanya's Tale" }, { name: "Players: Greece, USSR" }, { name: "Prison: miss" }, { name: "Warfactory: weap.infiltratable" }, { name: "Truk: truk.mission" }, { name: "TrukWaypoint1: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 89, name: "rules.yaml", path: "allies-05c/", nodeType: "db", pos: { x: 850, y: 8750 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: allies05c.lua" }, { name: "           allies05c-AI.lua" }, { name: "BriefingVideo: ally5.vqa" }, { name: "WEAP.infiltratable: ..." } ] },
        { id: 90, name: "map.yaml", path: "allies-10a/", nodeType: "db", pos: { x: 850, y: 9050 }, icon: "🗺️", columns: [ { name: "Title: Suspicion" }, { name: "Players: Greece, USSR, BadGuy" }, { name: "CommandCenter: fcom" }, { name: "MissileSilo1: mslo" }, { name: "FCom: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 91, name: "rules.yaml", path: "allies-10a/", nodeType: "db", pos: { x: 850, y: 9350 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: allies10a.lua" }, { name: "           allies10a-AI.lua" }, { name: "BriefingVideo: ally10.vqa" }, { name: "MCV: Buildable: ~disabled" } ] },
        { id: 92, name: "map.yaml", path: "atreides-05/", nodeType: "db", pos: { x: 850, y: 9650 }, icon: "🗺️", columns: [ { name: "Title: Atreides 05" }, { name: "Players: Atreides, Harkonnen,.." }, { name: "HarkonnenBarracks: barracks" }, { name: "Starport: starport" }, { name: "HarkonnenRally1: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 93, name: "rules.yaml", path: "atreides-05/", nodeType: "db", pos: { x: 850, y: 9950 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: atreides05.lua" }, { name: "           atreides05-AI.lua" }, { name: "BriefingVideo: A_BR05_E.VQA" } ] },
        { id: 94, name: "map.yaml", path: "harkonnen-09a/", nodeType: "db", pos: { x: 850, y: 10250 }, icon: "🗺️", columns: [ { name: "Title: Harkonnen 09a" }, { name: "Players: Harkonnen, Atreides, Corrino" }, { name: "HMCV: mcv" }, { name: "APalace: palace" }, { name: "CStarport: starport" }, { name: "HarkonnenRally: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 95, name: "rules.yaml", path: "harkonnen-09a/", nodeType: "db", pos: { x: 850, y: 10550 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: harkonnen09a.lua" }, { name: "           harkonnen09a-AI.lua" }, { name: "BriefingVideo: H_BR09_E.VQA" } ] },
        { id: 96, name: "map.yaml", path: "ordos-05/", nodeType: "db", pos: { x: 850, y: 10850 }, icon: "🗺️", columns: [ { name: "Title: Ordos 05" }, { name: "Players: Ordos, AtreidesMainBase..." }, { name: "AConyard: construction_yard" }, { name: "AStarport: starport" }, { name: "AtreidesRally1: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 97, name: "rules.yaml", path: "ordos-05/", nodeType: "db", pos: { x: 850, y: 11150 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: ordos05.lua" }, { name: "           ordos05-AI.lua" }, { name: "BriefingVideo: O_BR05_E.VQA" } ] },
        { id: 98, name: "map.yaml", path: "soviet-04a/", nodeType: "db", pos: { x: 850, y: 11450 }, icon: "🗺️", columns: [ { name: "Title: Behind the Lines" }, { name: "RadarDome: dome" }, { name: "CYard: fact" }, { name: "village1: v11" }, { name: "StartPoint: waypoint" }, { name: "Rules: rules.yaml" } ] },
        { id: 99, name: "rules.yaml", path: "soviet-04a/", nodeType: "db", pos: { x: 850, y: 11750 }, icon: "🔧", columns: [ { name: "LuaScript:" }, { name: "  Scripts: soviet04a.lua" }, { name: "           soviet04a-AI.lua" }, { name: "BriefingVideo: soviet4.vqa" }, { name: "MCV: Buildable: ~disabled" } ] },
        { id: 100, name: "mod.yaml (Mod Manifest)", path: "mods/ra/mod.yaml", nodeType: "db", pos: { x: 850, y: 12050 }, icon: "📦", columns: [ { name: "Rules: [...]" }, { name: "Sequences: [...]" }, { name: "Missions: missions.yaml" } ] },
        { id: 101, name: "map.yaml (Instance Data)", path: "maps/1ice6/", nodeType: "db", pos: { x: 850, y: 12350 }, icon: "🗺️", columns: [ { name: "RequiresMod: ts" }, { name: "Tileset: SNOW" }, { name: "Players: Multi0, Multi1..." }, { name: "Actors: (400+ items)" }, { name: "Actor0: aban03" }, { name: "Actor53: mutant" } ] },
        { id: 102, name: "GeoIP Database", path: "OpenRA.Game/Network/GeoIP.cs", nodeType: "service", pos: { x: 1250, y: 50 }, icon: "🌐", columns: [ { name: "LookupCountry()" }, { name: "fetches IP2LOCATION DB" } ] },
        { id: 103, name: "afld.shp", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 350 }, icon: "🖼️", columns: [ { name: "Sprite/Animation Data" } ] },
        { id: 104, name: "cliffsl1.tem", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 650 }, icon: "🎨", columns: [ { name: "Tileset Image Data" } ] },
        { id: 105, name: "civcapt1.aud", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 950 }, icon: "🔊", columns: [ { name: "Audio Data" } ] },
        { id: 106, name: "snow.mix", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 1250 }, icon: "📦", columns: [ { name: "Package Archive" } ] },
        { id: 107, name: "snow.pal", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 1550 }, icon: "🎨", columns: [ { name: "Color Palette" } ] },
        { id: 108, name: "e1.shp", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 1850 }, icon: "🖼️", columns: [ { name: "Infantry Sprite Data" } ] },
        { id: 109, name: "mcv.shp", path: "mods/cnc/bits/", nodeType: "service", pos: { x: 1250, y: 2150 }, icon: "🖼️", columns: [ { name: "MCV Sprite Data" } ] },
        { id: 110, name: "desert.pal", path: "mods/cnc/palettes/", nodeType: "service", pos: { x: 1250, y: 2450 }, icon: "🎨", columns: [ { name: "Color Palette" } ] },
        { id: 111, name: "ally8.vqa", path: "(videos)/", nodeType: "service", pos: { x: 1250, y: 2750 }, icon: "🎬", columns: [ { name: "Briefing Video Asset" } ] },
        { id: 112, name: "map.bin", path: "allies-10a/", nodeType: "service", pos: { x: 1250, y: 3050 }, icon: "▦", columns: [ { name: "Binary Terrain Data" } ] },
        { id: 113, name: "ally10.vqa", path: "(videos)/", nodeType: "service", pos: { x: 1250, y: 3350 }, icon: "🎬", columns: [ { name: "Briefing Video Asset" } ] },
        { id: 114, name: "map.bin", path: "atreides-05/", nodeType: "service", pos: { x: 1250, y: 3650 }, icon: "▦", columns: [ { name: "Binary Terrain Data" } ] },
        { id: 115, name: "A_BR05_E.VQA", path: "(videos)/", nodeType: "service", pos: { x: 1250, y: 3950 }, icon: "🎬", columns: [ { name: "Briefing Video Asset" } ] },
        { id: 116, name: "map.bin", path: "harkonnen-09a/", nodeType: "service", pos: { x: 1250, y: 4250 }, icon: "▦", columns: [ { name: "Binary Terrain Data" } ] },
        { id: 117, name: "H_BR09_E.VQA", path: "(videos)/", nodeType: "service", pos: { x: 1250, y: 4550 }, icon: "🎬", columns: [ { name: "Briefing Video Asset" } ] },
        { id: 118, name: "map.bin", path: "ordos-05/", nodeType: "service", pos: { x: 1250, y: 4850 }, icon: "▦", columns: [ { name: "Binary Terrain Data" } ] },
        { id: 119, name: "O_BR05_E.VQA", path: "(videos)/", nodeType: "service", pos: { x: 1250, y: 5150 }, icon: "🎬", columns: [ { name: "Briefing Video Asset" } ] }
    ],
    relationships: [
        { from: { table: "OpenRA.Launcher", column: "Main(string[] args)" }, to: { table: "Game.cs", column: "InitializeAndRun()" } },
        { from: { table: "WidgetLoader.cs", column: "LoadWidget()" }, to: { table: "MiniYaml.cs", column: "FromFile()" } },
        { from: { table: "Game.cs", column: "LogicTick()" }, to: { table: "Widget System", column: "Ui.Tick()" } },
        { from: { table: "Game.cs", column: "RenderTick()" }, to: { table: "Widget System", column: "Ui.Draw()" } },
        { from: { table: "Game.cs", column: "LogicTick()" }, to: { table: "OrderManager.cs", column: "TryTick()" } },
        { from: { table: "OrderManager.cs", column: "TryTick()" }, to: { table: "World.cs", column: "Tick()" } },
        { from: { table: "World.cs", column: "Tick()" }, to: { table: "Actor.cs", column: "Tick()" } },
        { from: { table: "Actor.cs", column: "Tick()" }, to: { table: "Activity.cs", column: "TickOuter()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "Manifest.cs (Mod Definition)", column: "Rules" } },
        { from: { table: "Manifest.cs (Mod Definition)", column: "Rules" }, to: { table: "MiniYaml.cs", column: "FromStream()" } },
        { from: { table: "MiniYaml.cs", column: "Merge()" }, to: { table: "Ruleset.cs", column: "LoadDefaults()" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "ActorInfo.cs", column: "Name" } },
        { from: { table: "ActorInfo.cs", column: "TraitsInConstructOrder()" }, to: { table: "TraitInfo.cs", column: "Create(ActorInitializer)" } },
        { from: { table: "World.cs", column: "CreateActor()" }, to: { table: "ActorInfo.cs", column: "TraitsInConstructOrder()" } },
        { from: { table: "World.cs", column: "CreateActor()" }, to: { table: "Actor.cs", column: "Tick()" } },
        { from: { table: "Actor.cs", column: "TraitsImplementing<T>()" }, to: { table: "TraitDictionary.cs", column: "WithInterface<T>()" } },
        { from: { table: "TraitDictionary.cs", column: "AddTrait()" }, to: { table: "TraitInfo.cs", column: "Create(ActorInitializer)" } },
        { from: { table: "OrderManager.cs", column: "ReceiveOrders()" }, to: { table: "Connection.cs", column: "Receive()" } },
        { from: { table: "Connection.cs", column: "Send()" }, to: { table: "Order.cs", column: "Serialize()" } },
        { from: { table: "OrderManager.cs", column: "IssueOrder()" }, to: { table: "Order.cs", column: "OrderString" } },
        { from: { table: "Actor.cs", column: "ResolveOrder()" }, to: { table: "Order.cs", column: "Subject" } },
        { from: { table: "Game.cs", column: "RenderTick()" }, to: { table: "WorldRenderer.cs", column: "Draw()" } },
        { from: { table: "WorldRenderer.cs", column: "PrepareRenderables()" }, to: { table: "World.cs", column: "Actors" } },
        { from: { table: "WorldRenderer.cs", column: "Draw()" }, to: { table: "Map.cs", column: "Tiles (CellLayer)" } },
        { from: { table: "Sandworm.cs (Mod Trait)", column: "RescanForTargets()" }, to: { table: "AttractsWorms.cs (Mod Trait)", column: "AttractionAtPosition()" } },
        { from: { table: "Sandworm.cs (Mod Trait)", column: "RescanForTargets()" }, to: { table: "Actor.cs", column: "Tick()" } },
        { from: { table: "World.cs", column: "Tick()" }, to: { table: "Sandworm.cs (Mod Trait)", column: "Tick()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "GeoIP Database", column: "fetches IP2LOCATION DB" } },
        { from: { table: "OpenRA.Launcher", column: "Main(string[] args)" }, to: { table: "Game.cs", column: "InitializeAndRun()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "MiniYaml.cs", column: "FromFile()" } },
        { from: { table: "MiniYaml.cs", column: "FromFile()" }, to: { table: "temperat.yaml", column: "General (Tileset Def)" } },
        { from: { table: "MiniYaml.cs", column: "FromFile()" }, to: { table: "ai.yaml", column: "ModularBot Definitions" } },
        { from: { table: "MiniYaml.cs", column: "FromFile()" }, to: { table: "aircraft.yaml", column: "TRAN (Transport)" } },
        { from: { table: "MiniYaml.cs", column: "Merge()" }, to: { table: "Ruleset.cs", column: "LoadDefaults()" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "ActorInfo.cs", column: "Name" } },
        { from: { table: "temperat.yaml", column: "Templates (Tile Rules)" }, to: { table: "cliffsl1.tem", column: "Tileset Image Data" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "afld.shp", column: "Sprite/Animation Data" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "snow.pal", column: "Color Palette" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "snow.mix", column: "Package Archive" } },
        { from: { table: "campaign.lua", column: "ReinforceWithLandingCraft()" }, to: { table: "Actor.cs", column: "CreateActor()" } },
        { from: { table: "campaign.lua", column: "ReinforceWithLandingCraft()" }, to: { table: "Actor.cs", column: "LoadPassenger()" } },
        { from: { table: "campaign.lua", column: "ReinforceWithLandingCraft()" }, to: { table: "Activity.cs", column: "ScriptedMove()" } },
        { from: { table: "campaign.lua", column: "ProduceUnits()" }, to: { table: "Actor.cs", column: "Build()" } },
        { from: { table: "campaign.lua", column: "CheckForBase()" }, to: { table: "World.cs", column: "GetActorsByType()" } },
        { from: { table: "Actor.cs", column: "ResolveOrder()" }, to: { table: "Order.cs", column: "Target" } },
        { from: { table: "World.cs", column: "CreateActor()" }, to: { table: "ActorInfo.cs", column: "TraitsInConstructOrder()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "Map.cs", column: "Actors (Definitions)" } },
        { from: { table: "mainmenu.yaml", column: "SINGLEPLAYER_BUTTON" }, to: { table: "lobby.yaml", column: "MAP_PREVIEW_ROOT" } },
        { from: { table: "lobby.yaml", column: "START_GAME_BUTTON" }, to: { table: "Game.cs", column: "InitializeAndRun()" } },
        { from: { table: "mainmenu.yaml", column: "SINGLEPLAYER_BUTTON" }, to: { table: "WidgetLoader.cs", column: "LoadWidget()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "nod09/map.yaml", column: "Title: Reinforce Egypt" } },
        { from: { table: "nod09/map.yaml", column: "Rules: nod09.lua" }, to: { table: "nod09.lua", column: "WorldLoaded()" } },
        { from: { table: "nod09.lua", column: "SendGDIAirstrike()" }, to: { table: "World.cs", column: "CreateActor()" } },
        { from: { table: "Game.cs", column: "InitializeAndRun()" }, to: { table: "Ruleset.cs", column: "LoadDefaults()" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "world.yaml", column: "Locomotor@FOOT" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "player.yaml", column: "^BasePlayer" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "infantry.yaml", column: "E1: ^Soldier" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "vehicles.yaml", column: "MCV: ^Vehicle" } },
        { from: { table: "Ruleset.cs", column: "LoadDefaults()" }, to: { table: "structures.yaml", column: "FACT: ^BaseBuilding" } },
        { from: { table: "World.cs", column: "CreateActor()" }, to: { table: "Ruleset.cs", column: "Actors (Dictionary)" } },
        { from: { table: "nod09/map.yaml", column: "Actors: ..." }, to: { table: "infantry.yaml", column: "E1: ^Soldier" } },
        { from: { table: "infantry.yaml", column: "E1: ^Soldier" }, to: { table: "infantry.yaml (Sequences)", column: "e1:" } },
        { from: { table: "vehicles.yaml", column: "MCV: ^Vehicle" }, to: { table: "vehicles.yaml (Sequences)", column: "mcv:" } },
        { from: { table: "infantry.yaml (Sequences)", column: "e1:" }, to: { table: "e1.shp", column: "Infantry Sprite Data" } },
        { from: { table: "vehicles.yaml (Sequences)", column: "mcv:" }, to: { table: "mcv.shp", column: "MCV Sprite Data" } },
        { from: { table: "nod09/map.yaml", column: "Tileset: DESERT" }, to: { table: "desert.pal", column: "Color Palette" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('gdi06')" }, to: { table: "map.yaml", column: "Title: Infiltrate Nod Base" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('gdi06')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: gdi06.lua" }, to: { table: "gdi06.lua", column: "WorldLoaded()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: gdi6.vqa" }, to: { table: "gdi6.vqa", column: "Briefing Video Asset" } },
        { from: { table: "rules.yaml", column: "MusicPlaylist: rain-ambient" }, to: { table: "rain-ambient.aud", column: "Ambient Audio Data" } },
        { from: { table: "gdi06.lua", column: "WorldLoaded()" }, to: { table: "campaign.lua", column: "InitObjectives(player)" } },
        { from: { table: "gdi06.lua", column: "IslandSamSites = {SAM01,..}" }, to: { table: "map.yaml", column: "SAM01: sam" } },
        { from: { table: "gdi06.lua", column: "unit.Patrol(FootPatrol1Route,...)" }, to: { table: "map.yaml", column: "waypoint10: waypoint" } },
        { from: { table: "gdi06.lua", column: "Trigger.OnAllKilled(IslandSamSites,..)" }, to: { table: "Actor.cs (Object)", column: "IsDead" } },
        { from: { table: "Actor.cs (Object)", column: "IsDead" }, to: { table: "gdi06.lua", column: "Trigger.OnAllKilled(IslandSamSites,..)" } },
        { from: { table: "gdi06.lua", column: "Trigger.OnAllKilled(IslandSamSites,..)" }, to: { table: "World.cs (State)", column: "CreateActor()" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('atreides05')" }, to: { table: "map.yaml", column: "Title: Atreides 05" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('atreides05')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: atreides05.lua" }, to: { table: "atreides05.lua", column: "WorldLoaded()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: A_BR05_E.VQA" }, to: { table: "A_BR05_E.VQA", column: "Briefing Video Asset" } },
        { from: { table: "atreides05.lua", column: "WorldLoaded()" }, to: { table: "campaign.lua", column: "InitObjectives(player)" } },
        { from: { table: "atreides05.lua", column: "WorldLoaded()" }, to: { table: "atreides05-AI.lua", column: "ActivateAI()" } },
        { from: { table: "atreides05.lua", column: "Trigger.OnCapture(Starport,...)" }, to: { table: "map.yaml", column: "Starport: starport" } },
        { from: { table: "atreides05.lua", column: "SendHarkonnen()" }, to: { table: "map.yaml", column: "HarkonnenRally1: waypoint" } },
        { from: { table: "atreides05-AI.lua", column: "ProduceInfantry()" }, to: { table: "World.cs (State)", column: "CreateActor()" } },
        { from: { table: "atreides05-AI.lua", column: "SendAttack()" }, to: { table: "Actor.cs (Object)", column: "AttackMove()" } },
        { from: { table: "atreides05.lua", column: "Trigger.OnCapture(Starport,...)" }, to: { table: "Actor.cs (Object)", column: "Capture()" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('harkonnen09a')" }, to: { table: "map.yaml", column: "Title: Harkonnen 09a" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('harkonnen09a')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: harkonnen09a.lua" }, to: { table: "harkonnen09a.lua", column: "WorldLoaded()" } },
        { from: { table: "harkonnen09a.lua", column: "ActivateAI()" }, to: { table: "harkonnen09a-AI.lua", column: "ActivateAI()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: H_BR09_E.VQA" }, to: { table: "H_BR09_E.VQA", column: "Briefing Video Asset" } },
        { from: { table: "harkonnen09a.lua", column: "BuildFremen()" }, to: { table: "map.yaml", column: "APalace: palace" } },
        { from: { table: "harkonnen09a.lua", column: "BuildFremen()" }, to: { table: "Actor.cs (Object)", column: "Produce()" } },
        { from: { table: "harkonnen09a.lua", column: "SendAirStrike()" }, to: { table: "Actor.cs (Object)", column: "TargetAirstrike()" } },
        { from: { table: "harkonnen09a-AI.lua", column: "ProduceUnits(AtreidesMain, ...)" }, to: { table: "World.cs (State)", column: "CreateActor()" } },
        { from: { table: "harkonnen09a.lua", column: "SendCarryallReinforcements(...)" }, to: { table: "map.yaml", column: "AtreidesRally1: waypoint" } },
        { from: { table: "harkonnen09a.lua", column: "SendCarryallReinforcements(...)" }, to: { table: "Actor.cs (Object)", column: "AttackMove()" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('ordos05')" }, to: { table: "map.yaml", column: "Title: Ordos 05" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('ordos05')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: ordos05.lua" }, to: { table: "ordos05.lua", column: "WorldLoaded()" } },
        { from: { table: "ordos05.lua", column: "ActivateAI()" }, to: { table: "ordos05-AI.lua", column: "ActivateAI()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: O_BR05_E.VQA" }, to: { table: "O_BR05_E.VQA", column: "Briefing Video Asset" } },
        { from: { table: "ordos05.lua", column: "Trigger.OnCapture(AStarport,...)" }, to: { table: "map.yaml", column: "AStarport: starport" } },
        { from: { table: "ordos05-AI.lua", column: "ProduceUnits(AtreidesMain,...)" }, to: { table: "map.yaml", column: "ABarracks1: barracks" } },
        { from: { table: "ordos05.lua", column: "SendCarryallReinforcements(...)" }, to: { table: "map.yaml", column: "AtreidesRally1: waypoint" } },
        { from: { table: "ordos05.lua", column: "Trigger.OnCapture(AStarport,...)" }, to: { table: "Actor.cs (Object)", column: "Capture()" } },
        { from: { table: "Actor.cs (Object)", column: "Capture()" }, to: { table: "ordos05.lua", column: "Trigger.OnCapture(AStarport,...)" } },
        { from: { table: "ordos05.lua", column: "Trigger.OnCapture(AStarport,...)" }, to: { table: "campaign.lua", column: "ReinforceWithTransport(...)" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('allies-06b')" }, to: { table: "map.yaml", column: "Title: Cripple Iron Curtain" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('allies-06b')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: allies06b.lua" }, to: { table: "allies06b.lua", column: "WorldLoaded()" } },
        { from: { table: "allies06b.lua", column: "ActivateAI()" }, to: { table: "allies06b-AI.lua", column: "ActivateAI()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: ally6.vqa" }, to: { table: "ally6.vqa", column: "Briefing Video Asset" } },
        { from: { table: "allies06b.lua", column: "InfiltrateTechCenter()" }, to: { table: "map.yaml", column: "TechLab1: stek" } },
        { from: { table: "allies06b-AI.lua", column: "ProduceVehicles()" }, to: { table: "map.yaml", column: "WarFactory: weap" } },
        { from: { table: "allies06b-AI.lua", column: "SendAttack(units, path)" }, to: { table: "map.yaml", column: "SovietBaseAttack: waypoint" } },
        { from: { table: "allies06b-AI.lua", column: "SendAttack(units, path)" }, to: { table: "Actor.cs (Object)", column: "AttackMove()" } },
        { from: { table: "allies06b.lua", column: "Trigger.OnInfiltrated(a, ...)" }, to: { table: "Actor.cs (Object)", column: "Infiltrate()" } },
        { from: { table: "Actor.cs (Object)", column: "Infiltrate()" }, to: { table: "allies06b.lua", column: "Trigger.OnInfiltrated(a, ...)" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('soviet-04a')" }, to: { table: "map.yaml", column: "Title: Behind the Lines" } },
        { from: { table: "Game.cs (Engine)", column: "LoadMap('soviet-04a')" }, to: { table: "map.bin", column: "Binary Terrain Data" } },
        { from: { table: "rules.yaml", column: "  Scripts: soviet04a.lua" }, to: { table: "soviet04a.lua", column: "WorldLoaded()" } },
        { from: { table: "soviet04a.lua", column: "RunInitialActivities()" }, to: { table: "soviet04a-AI.lua", column: "BuildBase()" } },
        { from: { table: "soviet04a.lua", column: "RunInitialActivities()" }, to: { table: "soviet04a-reinforcements.lua", column: "BringPatrol1()" } },
        { from: { table: "rules.yaml", column: "BriefingVideo: soviet4.vqa" }, to: { table: "soviet4.vqa", column: "Briefing Video Asset" } },
        { from: { table: "soviet04a.lua", column: "Trigger.OnKilled(RadarDome, ...)" }, to: { table: "map.yaml", column: "RadarDome: dome" } },
        { from: { table: "soviet04a-AI.lua", column: "BuildBuilding(building)" }, to: { table: "map.yaml", column: "GreeceCYard: waypoint" } },
        { from: { table: "soviet04a-AI.lua", column: "SendUnits(units, waypoints)" }, to: { table: "Actor.cs (Object)", column: "AttackMove()" } },
        { from: { table: "soviet04a-reinforcements.lua", column: "ReinfArmor()" }, to: { table: "soviet04a.lua", column: "Trigger.OnKilled(RadarDome, ...)" } }
    ]
};


// ===================================================================================
//  RENDERING LOGIC
// ===================================================================================
function initializeCanvas(canvasId, schema) {
    const canvas = document.getElementById(canvasId);
    if (!canvas) return;
    const transformContainer = canvas.querySelector('.transform-container');
    const svg = canvas.querySelector('.connections');
    let state = { scale: 0.7, panX: 50, panY: 50, isPanning: false, lastMouse: { x: 0, y: 0 } };

    function render() {
        if (!transformContainer || !svg) return;
        transformContainer.innerHTML = '';
        transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
        
        schema.tables.forEach(table => {
            const node = document.createElement('div');
            node.id = `${canvasId}-${table.id}`;
            node.classList.add('node', `${table.nodeType}-node`);
            node.style.left = `${table.pos.x}px`;
            node.style.top = `${table.pos.y}px`;

            const header = document.createElement('h3');
            const pathSpan = table.path ? `<span class="path">${table.path}</span>` : '';
            header.innerHTML = `${pathSpan}${table.name}`;

            const list = document.createElement('ul');
            list.innerHTML = table.columns.map(col => {
                const colName = typeof col === 'string' ? col : col.name;
                const colType = typeof col === 'string' ? '' : col.type;
                const colId = colName.replace(/\s+/g, '-').replace(/[^\w-]/g, '');
                return `<li id="${canvasId}-${table.id}-${colId}"><span class="col-name">${colName}</span>${colType ? `<span class="col-type">${colType}</span>` : ''}</li>`;
            }).join('');
            
            if (table.icon) {
                const iconDisplay = document.createElement('div');
                iconDisplay.className = 'icon-display';
                iconDisplay.textContent = table.icon;
                node.appendChild(iconDisplay);
            }

            node.appendChild(header);
            node.appendChild(list);
            transformContainer.appendChild(node);
        });
        updateConnections();
    }
    
    function getElementPortPosition(elId) {
        const el = document.getElementById(elId);
        if (!el) return null;
        const parentNode = el.closest('.node');
        if (!parentNode) return null;
        const isNodeConnection = el.classList.contains('node');
        
        const parentRect = parentNode.getBoundingClientRect();
        const elRect = isNodeConnection ? parentRect : el.getBoundingClientRect();
        const canvasRect = canvas.getBoundingClientRect();
        
        const y = isNodeConnection ? (parentRect.top - canvasRect.top + parentRect.height / 2) : (elRect.top - canvasRect.top + elRect.height / 2);
        const leftX = (parentRect.left - canvasRect.left);
        const rightX = (parentRect.right - canvasRect.left);

        return { left: {x: leftX, y: y}, right: {x: rightX, y: y} };
    }

    function updateConnections() {
        if (!svg) return;
        svg.innerHTML = `<defs>
            <marker id="arrowhead-read-${canvasId}" markerWidth="10" markerHeight="7" refX="8" refY="3.5" orient="auto"><polygon points="0 0, 10 3.5, 0 7" fill="#6b7283" /></marker>
            <marker id="arrowhead-write-${canvasId}" markerWidth="12" markerHeight="9" refX="10" refY="4.5" orient="auto"><polygon points="0 0, 12 4.5, 0 9" fill="#86efac" /></marker>
            <marker id="arrowhead-flow-${canvasId}" markerWidth="8" markerHeight="6" refX="7" refY="3" orient="auto"><polygon points="0 0, 8 3, 0 6" fill="#9ca3af" /></marker>
        </defs>`;
        
        const idMap = new Map(schema.tables.map(t => [t.name, t.id]));

        schema.relationships.forEach(rel => {
            const fromId = idMap.get(rel.from.table);
            const toId = idMap.get(rel.to.table);
            if(!fromId || !toId) return;

            let fromColName = typeof rel.from.column === 'string' ? rel.from.column : rel.from.column.name;
            let toColName = typeof rel.to.column === 'string' ? rel.to.column : rel.to.column.name;
            
            let fromElId = `${canvasId}-${fromId}-${fromColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}`;
            if (!document.getElementById(fromElId)) fromElId = `${canvasId}-${fromId}`;

            let toElId = `${canvasId}-${toId}-${toColName.replace(/\s+/g, '-').replace(/[^\w-]/g, '')}`;
            if (!document.getElementById(toElId)) toElId = `${canvasId}-${toId}`;
            
            const fromPorts = getElementPortPosition(fromElId);
            const toPorts = getElementPortPosition(toElId);
            if (!fromPorts || !toPorts) return;

            const fromPos = toPorts.right.x < fromPorts.left.x ? fromPorts.left : fromPorts.right;
            const toPos = toPorts.right.x < fromPorts.left.x ? toPorts.right : toPorts.left;
            
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', fromPos.x); line.setAttribute('y1', fromPos.y);
            line.setAttribute('x2', toPos.x); line.setAttribute('y2', toPos.y);

            if (rel.type === 'write') {
                line.setAttribute('stroke', '#86efac'); line.setAttribute('stroke-width', 4); line.setAttribute('marker-end', `url(#arrowhead-write-${canvasId})`);
            } else if (rel.type === 'flow') {
                line.setAttribute('stroke', '#9ca3af'); line.setAttribute('stroke-width', 2); line.setAttribute('stroke-dasharray', `6,6`); line.setAttribute('marker-end', `url(#arrowhead-flow-${canvasId})`);
            } else {
                line.setAttribute('stroke', '#6b7283'); line.setAttribute('stroke-width', 2); line.setAttribute('marker-end', `url(#arrowhead-read-${canvasId})`);
            }
            svg.appendChild(line);
        });
    }

    let activeNode = null, offset = { x: 0, y: 0 };
    canvas.addEventListener('mousedown', (e) => {
        const targetNode = e.target.closest('.node');
        if (targetNode) {
            activeNode = targetNode;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (!tableData) return;
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            offset.x = mouseX - tableData.pos.x;
            offset.y = mouseY - tableData.pos.y;
            activeNode.style.zIndex = 11;
        } else {
            state.isPanning = true;
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });

    document.addEventListener('mousemove', (e) => {
        if (activeNode) {
            e.preventDefault();
            const mouseX = (e.clientX - canvas.getBoundingClientRect().left - state.panX) / state.scale;
            const mouseY = (e.clientY - canvas.getBoundingClientRect().top - state.panY) / state.scale;
            const tableData = schema.tables.find(t => `${canvasId}-${t.id}` === activeNode.id);
            if (tableData) {
                tableData.pos.x = mouseX - offset.x;
                tableData.pos.y = mouseY - offset.y;
                activeNode.style.left = `${tableData.pos.x}px`;
                activeNode.style.top = `${tableData.pos.y}px`;
                updateConnections();
            }
        } else if (state.isPanning) {
            e.preventDefault();
            const dx = e.clientX - state.lastMouse.x;
            const dy = e.clientY - state.lastMouse.y;
            state.panX += dx;
            state.panY += dy;
            transformContainer.style.transform = `translate(${state.panX}px, ${state.panY}px) scale(${state.scale})`;
            updateConnections();
            state.lastMouse.x = e.clientX;
            state.lastMouse.y = e.clientY;
        }
    });
    
    document.addEventListener('mouseup', () => {
        if (activeNode) { activeNode.style.zIndex = 10; activeNode = null; }
        state.isPanning = false;
    });
    
    canvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        const rect = canvas.getBoundingClientRect();
        const mouseX = e.clientX - rect.left;
        const mouseY = e.clientY - rect.top;
        const oldScale = state.scale;
        const zoomFactor = 1.1;
        state.scale *= e.deltaY < 0 ? zoomFactor : 1 / zoomFactor;
        state.scale = Math.max(0.1, Math.min(state.scale, 2.5));
        state.panX = mouseX - (mouseX - state.panX) * (state.scale / oldScale);
        state.panY = mouseY - (mouseY - state.panY) * (state.scale / oldScale);
        render();
    });

    render();
    return { render, updateConnections };
}

const canvases = [
    initializeCanvas('canvas-r2', schemaR2),
    initializeCanvas('canvas-r3', schemaR3),
    initializeCanvas('canvas-r4', schemaR4)
];

document.querySelectorAll('.splitter').forEach(splitter => {
    splitter.addEventListener('mousedown', (e) => {
        e.preventDefault();
        const prevPanel = splitter.previousElementSibling;
        const startX = e.clientX;
        const initialPrevWidth = prevPanel.getBoundingClientRect().width;
        
        const onMouseMove = (moveEvent) => {
            let newPrevWidth = initialPrevWidth + (moveEvent.clientX - startX);
            const MIN_WIDTH = 150;
            if (newPrevWidth < MIN_WIDTH) newPrevWidth = MIN_WIDTH;
            prevPanel.style.flex = `0 0 ${newPrevWidth}px`;
            canvases.forEach(c => c && c.render());
        };
        const onMouseUp = () => {
            document.removeEventListener('mousemove', onMouseMove);
            document.removeEventListener('mouseup', onMouseUp);
        };
        document.addEventListener('mousemove', onMouseMove);
        document.addEventListener('mouseup', onMouseUp);
    });
});

window.addEventListener('resize', () => {
    canvases.forEach(c => c && c.render());
});
</script>

</body>
</html>