/* index.js

This file adds small enhancements to your GitHub Pages documentation:

1. Copy-to-clipboard buttons for all code blocks


2. Smooth scrolling for internal links



This is PURE JavaScript (no frameworks) Safe for GitHub Pages */

// Run after page loads document.addEventListener("DOMContentLoaded", () => { addCopyButtons(); enableSmoothScroll(); });

/* ---------------------------------- Copy-to-clipboard for code blocks ----------------------------------- */ function addCopyButtons() { const codeBlocks = document.querySelectorAll("pre");

codeBlocks.forEach((block) => { const button = document.createElement("button"); button.innerText = "Copy"; button.className = "copy-btn";

button.addEventListener("click", async () => {
  const code = block.innerText;
  await navigator.clipboard.writeText(code);
  button.innerText = "Copied ✓";

  setTimeout(() => {
    button.innerText = "Copy";
  }, 1500);
});

block.style.position = "relative";
block.appendChild(button);

}); }

/* ---------------------------------- Smooth scrolling for anchor links ----------------------------------- */ function enableSmoothScroll() { const links = document.querySelectorAll('a[href^="#"]');

links.forEach((link) => { link.addEventListener("click", (e) => { e.preventDefault(); const targetId = link.getAttribute("href").substring(1); const target = document.getElementById(targetId);

if (target) {
    target.scrollIntoView({ behavior: "smooth" });
  }
});

}); }

/* ---------------------------------- Optional basic styles (JS-injected) ----------------------------------- */ const style = document.createElement("style"); style.innerHTML = ` .copy-btn { position: absolute; top: 8px; right: 8px; font-size: 12px; padding: 4px 8px; border: none; border-radius: 4px; cursor: pointer; background: #2d2d2d; color: #fff; opacity: 0.8; }

.copy-btn:hover { opacity: 1; } `;

document.head.appendChild(style);
