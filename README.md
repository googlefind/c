// Replace the form submit handler with:
document.getElementById('codeForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const code = document.getElementById('codeInput').value.trim();
    const language = document.getElementById('language').value;
    
    if (code) {
        try {
            const response = await fetch('/api/codes', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ code, language }),
            });
            const newCode = await response.json();
            addCodeSnippet(newCode.code, newCode.language);
            document.getElementById('codeInput').value = '';
        } catch (error) {
            console.error('Error:', error);
        }
    }
});

// Add this to load existing codes when page loads
window.addEventListener('DOMContentLoaded', async () => {
    try {
        const response = await fetch('/api/codes');
        const codes = await response.json();
        codes.forEach(code => {
            addCodeSnippet(code.code, code.language);
        });
    } catch (error) {
        console.error('Error loading codes:', error);
    }
});
