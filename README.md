# ViralTube-Keyword-Pro
## AI Hustle Hub – A secure, modern web &amp; mobile app that helps users discover AI tools, explore daily side hustle ideas, and track opportunities to earn online. Built with Next.js, Firebase, and AI-powered recommendations ##
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube SEO Keyword Generator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f9fb;
            color: #1f2937;
        }
        .container {
            max-width: 800px;
        }
        /* Style for the main, file-generating button */
        .youtube-btn {
            background-color: #ff0000;
            transition: all 0.2s ease;
        }
        .youtube-btn:hover {
            background-color: #cc0000;
            box-shadow: 0 4px 15px rgba(255, 0, 0, 0.4);
        }
        /* Style for the new, AI-powered feature buttons */
        .ai-feature-btn {
            background-color: #3b82f6; /* Blue for new features */
            transition: all 0.2s ease;
        }
        .ai-feature-btn:hover {
            background-color: #2563eb;
            box-shadow: 0 4px 15px rgba(59, 130, 246, 0.4);
        }
        .result-box {
            border: 1px solid #e5e7eb;
            background-color: #ffffff;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            min-height: 250px;
        }
        /* Styling for Markdown output */
        .markdown-output h3 {
            font-size: 1.25rem;
            font-weight: 700;
            margin-top: 1.5rem;
            margin-bottom: 0.5rem;
            color: #1f2937;
            border-bottom: 2px solid #ff0000;
            padding-bottom: 4px;
        }
        .markdown-output ul {
            list-style: disc;
            padding-left: 1.5rem;
            margin-bottom: 1rem;
        }
        .markdown-output li {
            margin-bottom: 0.25rem;
            line-height: 1.4;
        }
        .markdown-output p {
            margin-bottom: 1rem;
        }
        #loading-indicator {
            border-top-color: #ff0000;
            -webkit-animation: spinner 1.5s linear infinite;
            animation: spinner 1.5s linear infinite;
        }

        @-webkit-keyframes spinner {
            0% { -webkit-transform: rotate(0deg); }
            100% { -webkit-transform: rotate(360deg); }
        }

        @keyframes spinner {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

    </style>
</head>
<body class="p-4 md:p-8">

    <div class="container mx-auto">
        <header class="text-center mb-8">
            <h1 class="text-4xl font-extrabold text-[#ff0000] mb-2">
                ViralTube Keyword Pro
            </h1>
            <p class="text-lg text-gray-600">Research Keywords & Hashtags for Maximum Reach</p>
        </header>

        <!-- Input and Button Area -->
        <div class="bg-white p-6 rounded-xl shadow-lg mb-8">
            <label for="video-topic" class="block text-xl font-semibold mb-3 text-gray-800">
                What is your video about? (Topic or Title)
            </label>
            <input
                type="text"
                id="video-topic"
                placeholder="e.g., 'How to train a puppy in 5 minutes' or 'Best gaming mouse review 2025'"
                class="w-full p-3 border-2 border-gray-300 rounded-lg focus:border-[#ff0000] focus:ring-0 text-lg mb-4"
                autocomplete="off"
            >
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <!-- Main Keyword Generator Button (File Output) -->
                <button
                    id="generate-btn"
                    class="youtube-btn col-span-1 md:col-span-1 text-white font-bold py-3 px-4 rounded-lg flex items-center justify-center text-lg transition duration-200 ease-in-out"
                    onclick="generateContent('keywords')"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
                    </svg>
                    1. Generate Keywords & Title
                </button>

                <!-- New Feature 1: Description Draft -->
                <button
                    id="generate-description-btn"
                    class="ai-feature-btn col-span-1 text-white font-bold py-3 px-4 rounded-lg flex items-center justify-center text-lg transition duration-200 ease-in-out"
                    onclick="generateContent('description')"
                >
                    ✨ Generate SEO Description Draft
                </button>

                <!-- New Feature 2: Content Ideas -->
                <button
                    id="generate-ideas-btn"
                    class="ai-feature-btn col-span-1 text-white font-bold py-3 px-4 rounded-lg flex items-center justify-center text-lg transition duration-200 ease-in-out"
                    onclick="generateContent('ideas')"
                >
                    ✨ Brainstorm Related Video Ideas
                </button>
            </div>
        </div>

        <!-- Results and Loading Area -->
        <div class="result-box p-6 rounded-xl relative">
            <div id="loading-indicator" class="hidden absolute inset-0 flex items-center justify-center bg-white bg-opacity-80 rounded-xl">
                <div class="w-12 h-12 border-4 border-gray-200 border-solid rounded-full animate-spin"></div>
                <p class="ml-4 text-xl font-medium text-[#ff0000]">
                    AI is working on your request...
                </p>
            </div>

            <div id="results-content" class="markdown-output">
                <p class="text-gray-500 text-center py-10">
                    Enter your video topic above and click a button to begin generating content strategy.
                </p>
            </div>

            <div id="download-area" class="mt-4 text-center hidden">
                <p class="text-sm text-gray-500 mb-2">This file contains the Title, Keywords, and Hashtags.</p>
                <button
                    id="download-btn"
                    class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded-lg transition duration-200 ease-in-out"
                    onclick="downloadResults()"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline mr-2" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L10 11.586l2.293-2.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z" clip-rule="evenodd" />
                    </svg>
                    Download Keywords/Title as TXT File
                </button>
            </div>

             <!-- Citation Display Area -->
            <div id="citations" class="mt-6 text-sm text-gray-500 border-t pt-4 hidden">
                <h4 class="font-semibold mb-2">Sources Used for Research:</h4>
                <ul id="citation-list" class="space-y-1"></ul>
            </div>
        </div>
    </div>

    <script type="module">
        // Global variables provided by the environment
        const apiKey = ""; // API key is handled by the Canvas environment

        const apiUrl = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent";

        const inputField = document.getElementById('video-topic');
        const generateBtn = document.getElementById('generate-btn');
        const generateDescriptionBtn = document.getElementById('generate-description-btn');
        const generateIdeasBtn = document.getElementById('generate-ideas-btn');
        const loadingIndicator = document.getElementById('loading-indicator');
        const resultsContent = document.getElementById('results-content');
        const downloadArea = document.getElementById('download-area');
        const citations = document.getElementById('citations');
        const citationList = document.getElementById('citation-list');

        let rawMarkdownOutput = ""; // Stores the generated text for download (Only used by the Keyword function)

        /**
         * Converts Markdown text to HTML for display, focusing on lists and headers.
         * @param {string} markdown - The markdown string from the API.
         * @returns {string} The HTML formatted string.
         */
        function markdownToHtml(markdown) {
            // Replace **bold** with <strong>
            let html = markdown.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
            
            // Convert ### headers to <h3>
            html = html.replace(/###\s*(.*)/g, '<h3>$1</h3>');

            // Convert lists (* or -) to <ul><li>
            html = html.replace(/^- (.*)/gm, '<li>$1</li>');
            html = html.replace(/\* (.*)/gm, '<li>$1</li>');
            
            // Wrap list items in <ul> blocks, ensuring multiple blocks are handled
            html = html.replace(/(<li>.*?<\/li>\s*)+/gs, '<ul>$&</ul>');
            
            // Remove any empty <ul></ul> tags that might result
            html = html.replace(/<ul>\s*<\/ul>/g, '');

            // Convert paragraphs
            html = markdown.replace(/([^<Hh\n][^\n]+)/g, '<p>$1</p>'); // Use markdown variable here for full content
            
            // Clean up multiple <p> tags and single newlines in paragraphs
            html = html.replace(/<p>\s*(<h3>|<ul>)/g, '$1');
            html = html.replace(/(<\/ul>|<\/h3>)\s*<\/p>/g, '$1');

            return html;
        }

        /**
         * Sets the UI state to loading.
         * @param {string} message - The message to display during loading.
         */
        function setLoadingState(message) {
            resultsContent.innerHTML = '';
            downloadArea.classList.add('hidden');
            citations.classList.add('hidden');
            loadingIndicator.classList.remove('hidden');
            document.querySelectorAll('button').forEach(btn => btn.disabled = true);
            
            const loadingText = loadingIndicator.querySelector('p');
            loadingText.textContent = message;
        }

        /**
         * Resets the UI state after loading.
         */
        function resetLoadingState() {
            loadingIndicator.classList.add('hidden');
            document.querySelectorAll('button').forEach(btn => btn.disabled = false);
        }

        /**
         * Handles the API call for various functions (keywords, description, ideas).
         * @param {string} mode - The generation mode ('keywords', 'description', or 'ideas').
         */
        window.generateContent = async function(mode) {
            const userQuery = inputField.value.trim();
            if (!userQuery) {
                resultsContent.innerHTML = '<p class="text-red-500 text-center py-10">Please enter a video topic to begin.</p>';
                return;
            }

            setLoadingState(mode === 'keywords' ? 'Researching Google & YouTube Trends...' : 
                            mode === 'description' ? 'Drafting SEO Description...' : 
                            'Brainstorming Related Content...');

            let systemPrompt = "";
            let useGrounding = false;

            if (mode === 'keywords') {
                systemPrompt = `You are a world-class YouTube SEO specialist focused on viral video strategy. The user is providing a video topic and needs high-ranking keywords, hashtags, and a killer title. Use the Google Search results to find trending topics, search volume, and competitor strategies. Structure your response clearly using Markdown under these four mandatory headings in this order: "Viral Video Title Suggestion", "High-Ranking Keywords (for the video title and description)", "Strategic Long-Tail Keywords (for description and tags)", and "Top Trending Hashtags (for tags)". 
- The title suggestion should be concise, attention-grabbing, and optimized for click-through rate (CTR) and searchability.
- All keyword and hashtag lists must use bullet points (* or -) and reflect real-time search demand and ranking potential for YouTube.`;
                useGrounding = true;
            } else if (mode === 'description') {
                 // No grounding needed, LLM drafts based on internal knowledge and the topic
                 systemPrompt = `You are an expert YouTube copywriter. Draft a full, SEO-optimized video description for the topic: "${userQuery}". The description should be structured as follows using Markdown:
- Paragraph 1: A strong hook and summary of the video.
- Paragraph 2: Details about what the viewer will learn, including a call to action.
- Paragraph 3: Recommended gear/tools section (if applicable, otherwise generalize).
- Must include a separate list of 10-15 keywords naturally integrated into the text. Do not use hashtags.`;
                 useGrounding = false;
            } else if (mode === 'ideas') {
                systemPrompt = `You are a YouTube content strategist. Based on the user's video topic, "${userQuery}", research related trending or evergreen content ideas for a cohesive video series. Provide a list of 5-7 unique video ideas. Structure the output using Markdown with one main heading: "Next Video Series Ideas", followed by a bulleted list where each item is a complete, optimized video title and a brief one-sentence concept.`;
                useGrounding = true;
            }

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                tools: useGrounding ? [{ "google_search": {} }] : undefined,
                systemInstruction: { parts: [{ text: systemPrompt }] },
            };

            const url = `${apiUrl}?key=${apiKey}`;

            try {
                let response;
                let maxRetries = 3;
                let delay = 1000;

                for (let i = 0; i < maxRetries; i++) {
                    response = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (response.ok) {
                        break; // Success
                    }

                    if (i < maxRetries - 1) {
                        await new Promise(resolve => setTimeout(resolve, delay));
                        delay *= 2; // Exponential backoff
                    } else {
                        throw new Error(`API call failed after ${maxRetries} attempts.`);
                    }
                }

                const result = await response.json();
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    const generatedText = candidate.content.parts[0].text;
                    
                    // 2. Handle display based on mode
                    resultsContent.innerHTML = markdownToHtml(generatedText);
                    
                    if (mode === 'keywords') {
                        rawMarkdownOutput = generatedText;
                        downloadArea.classList.remove('hidden');
                    } else {
                        // Clear download area for non-keyword results
                        downloadArea.classList.add('hidden');
                    }

                    // 3. Extract and display citations (only if grounding was used)
                    citationList.innerHTML = '';
                    let sources = [];
                    const groundingMetadata = candidate.groundingMetadata;
                    if (useGrounding && groundingMetadata && groundingMetadata.groundingAttributions) {
                        sources = groundingMetadata.groundingAttributions
                            .map(attribution => ({
                                uri: attribution.web?.uri,
                                title: attribution.web?.title,
                            }))
                            .filter(source => source.uri && source.title);
                    }

                    if (sources.length > 0) {
                        citations.classList.remove('hidden');
                        sources.forEach(source => {
                            const li = document.createElement('li');
                            li.innerHTML = `<a href="${source.uri}" target="_blank" class="text-blue-600 hover:text-blue-800 hover:underline" title="${source.uri}">${source.title}</a>`;
                            citationList.appendChild(li);
                        });
                    } else {
                         citations.classList.add('hidden');
                    }

                } else {
                    resultsContent.innerHTML = '<p class="text-red-500 text-center py-10">Error: Could not retrieve suggestions. Please try again or refine your query.</p>';
                    console.error("Gemini API returned no text content:", result);
                }

            } catch (error) {
                resultsContent.innerHTML = `<p class="text-red-500 text-center py-10">An unexpected error occurred: ${error.message}.</p>`;
                console.error("Fetch error:", error);
            } finally {
                // 4. Reset UI
                resetLoadingState();
            }
        }

        /**
         * Downloads the raw markdown output as a .txt file (only for keyword mode).
         */
        window.downloadResults = function() {
            if (!rawMarkdownOutput) {
                const messageBox = document.getElementById('results-content');
                messageBox.innerHTML = '<p class="text-red-500 text-center py-10">Cannot download: No keyword results have been generated yet. Please click "Generate Keywords & Title".</p>';
                return;
            }

            const fileName = 'YouTube_Keywords_Hashtags.txt';
            const blob = new Blob([rawMarkdownOutput], { type: 'text/plain;charset=utf-8' });
            
            // Create a temporary link element
            const a = document.createElement('a');
            a.href = URL.createObjectURL(blob);
            a.download = fileName;
            
            // Append to body, click, and remove
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
        }
    </script>
</body>
</html>


