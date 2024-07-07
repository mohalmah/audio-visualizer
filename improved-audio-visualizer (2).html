<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audio Visualizer with Dual Visualization Options</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: #000;
            font-family: Arial, sans-serif;
            color: white;
        }
        #visualizer {
            width: 100%;
            height: 100%;
        }
        #controls {
            position: absolute;
            top: 10px;
            left: 10px;
            z-index: 10;
        }
        #fileInput {
            display: none;
        }
        label, button, a.button {
            background-color: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            border-radius: 20px;
        }
        #customText {
            background-color: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: 5px;
            margin: 4px 2px;
            border-radius: 5px;
        }
        #greenScreenToggle, #visualizationToggle {
            margin-left: 10px;
        }
        #downloadLink {
            display: none;
        }
        #loadingIndicator {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
            z-index: 100;
        }
        #errorMessage {
            display: none;
            color: red;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div id="controls">
        <label for="fileInput">Choose Audio</label>
        <input type="file" id="fileInput" accept="audio/*">
        <button id="playPauseBtn">Play</button>
        <button id="generateBtn">Generate Video</button>
        <a id="downloadLink" class="button" download="visualization.webm">Download Video</a>
        <input type="text" id="customText" placeholder="Custom Text" value="AUDIO VISUALIZER">
        <label for="greenScreenToggle">Green Screen</label>
        <input type="checkbox" id="greenScreenToggle">
        <label for="visualizationToggle">Simple Waveform</label>
        <input type="checkbox" id="visualizationToggle">
    </div>
    <canvas id="visualizer"></canvas>
    <div id="loadingIndicator">Generating video... Please wait.</div>
    <div id="errorMessage"></div>

    <script>
        const canvas = document.getElementById('visualizer');
        const ctx = canvas.getContext('2d');
        const fileInput = document.getElementById('fileInput');
        const playPauseBtn = document.getElementById('playPauseBtn');
        const generateBtn = document.getElementById('generateBtn');
        const downloadLink = document.getElementById('downloadLink');
        const customTextInput = document.getElementById('customText');
        const greenScreenToggle = document.getElementById('greenScreenToggle');
        const visualizationToggle = document.getElementById('visualizationToggle');
        const loadingIndicator = document.getElementById('loadingIndicator');
        const errorMessage = document.getElementById('errorMessage');

        let audioContext, analyser, source, audioBuffer;
        let isPlaying = false;
        let animationFrame;

        // Set canvas size to Full HD
        canvas.width = 1920;
        canvas.height = 1080;

        // Initialize audio context
        audioContext = new (window.AudioContext || window.webkitAudioContext)();

        function initAudio(buffer) {
            audioBuffer = buffer;
            analyser = audioContext.createAnalyser();
            analyser.fftSize = 2048;
            
            source = audioContext.createBufferSource();
            source.buffer = audioBuffer;
            source.connect(analyser);
            analyser.connect(audioContext.destination);
        }

        function drawCircularVisualization(frequencyData) {
            const width = canvas.width;
            const height = canvas.height;

            const centerX = width / 2;
            const centerY = height / 2;
            const baseRadius = Math.min(width, height) * 0.2;
            const maxSpikeLength = Math.min(width, height) * 0.3;

            ctx.fillStyle = greenScreenToggle.checked ? '#00FF00' : 'rgba(0, 0, 0, 1)';
            ctx.fillRect(0, 0, width, height);

            const totalSpikes = frequencyData.length;
            for (let i = 0; i < totalSpikes; i++) {
                const angle = (i / totalSpikes) * Math.PI * 2;
                const amplitude = frequencyData[i] / 255;
                const spikeLength = baseRadius + amplitude * maxSpikeLength;

                const gradient = ctx.createRadialGradient(centerX, centerY, baseRadius, centerX, centerY, spikeLength);
                gradient.addColorStop(0, 'rgba(0, 0, 255, 0.8)');
                gradient.addColorStop(0.5, 'rgba(255, 165, 0, 0.5)');
                gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');

                ctx.beginPath();
                ctx.moveTo(centerX + baseRadius * Math.cos(angle), centerY + baseRadius * Math.sin(angle));
                ctx.lineTo(centerX + spikeLength * Math.cos(angle), centerY + spikeLength * Math.sin(angle));
                ctx.strokeStyle = gradient;
                ctx.lineWidth = 4;
                ctx.stroke();
            }

            ctx.beginPath();
            ctx.arc(centerX, centerY, baseRadius, 0, Math.PI * 2);
            ctx.fillStyle = 'rgba(0, 0, 0, 0.8)';
            ctx.fill();
            ctx.strokeStyle = 'rgba(255, 165, 0, 0.8)';
            ctx.lineWidth = 4;
            ctx.stroke();

            ctx.fillStyle = 'white';
            ctx.font = `${baseRadius * 0.2}px Arial`;
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            const lines = customTextInput.value.split('\n');
            lines.forEach((line, index) => {
                ctx.fillText(line, centerX, centerY + (index - (lines.length - 1) / 2) * baseRadius * 0.25);
            });
        }

        function drawWaveformVisualization(timeData) {
            const width = canvas.width;
            const height = canvas.height;

            ctx.fillStyle = 'black';
            ctx.fillRect(0, 0, width, height);

            ctx.lineWidth = 2;
            ctx.strokeStyle = 'white';
            ctx.beginPath();

            const sliceWidth = width / timeData.length;
            let x = 0;

            for (let i = 0; i < timeData.length; i++) {
                const v = timeData[i] / 128.0;
                const y = (v * height) / 2;

                if (i === 0) {
                    ctx.moveTo(x, y);
                } else {
                    ctx.lineTo(x, y);
                }

                x += sliceWidth;
            }

            ctx.lineTo(width, height / 2);
            ctx.stroke();
        }

        function drawVisualization() {
            const frequencyData = new Uint8Array(analyser.frequencyBinCount);
            const timeData = new Uint8Array(analyser.frequencyBinCount);
            analyser.getByteFrequencyData(frequencyData);
            analyser.getByteTimeDomainData(timeData);

            if (visualizationToggle.checked) {
                drawWaveformVisualization(timeData);
            } else {
                drawCircularVisualization(frequencyData);
            }
        }

        async function generateVideo() {
            loadingIndicator.style.display = 'block';
            generateBtn.disabled = true;
            errorMessage.style.display = 'none';

            try {
                const stream = canvas.captureStream(60);
                const audioTracks = audioContext.createMediaStreamDestination().stream.getAudioTracks();
                const combinedStream = new MediaStream([...stream.getTracks(), ...audioTracks]);

                const mediaRecorder = new MediaRecorder(combinedStream, {
                    mimeType: 'video/webm;codecs=vp9,opus',
                    videoBitsPerSecond: 8000000
                });

                const chunks = [];
                mediaRecorder.ondataavailable = e => chunks.push(e.data);
                mediaRecorder.onstop = async () => {
                    const blob = new Blob(chunks, { type: 'video/webm' });
                    const url = URL.createObjectURL(blob);
                    downloadLink.href = url;
                    downloadLink.style.display = 'inline-block';
                    loadingIndicator.style.display = 'none';
                    generateBtn.disabled = false;
                };

                mediaRecorder.start();

                source = audioContext.createBufferSource();
                source.buffer = audioBuffer;
                source.connect(analyser);
                source.connect(audioContext.destination);
                source.start(0);

                function animate() {
                    drawVisualization();
                    animationFrame = requestAnimationFrame(animate);
                }
                animate();

                source.onended = () => {
                    cancelAnimationFrame(animationFrame);
                    mediaRecorder.stop();
                };

            } catch (error) {
                console.error('Error in video generation:', error);
                errorMessage.textContent = `Error: ${error.message}`;
                errorMessage.style.display = 'block';
                loadingIndicator.style.display = 'none';
                generateBtn.disabled = false;
            }
        }

        fileInput.addEventListener('change', (event) => {
            const file = event.target.files[0];
            const reader = new FileReader();

            reader.onload = async (e) => {
                try {
                    const buffer = await audioContext.decodeAudioData(e.target.result);
                    initAudio(buffer);
                    playPauseBtn.disabled = false;
                    generateBtn.disabled = false;
                    errorMessage.style.display = 'none';
                } catch (error) {
                    console.error('Error decoding audio data:', error);
                    errorMessage.textContent = 'Error loading audio file. Please try another file.';
                    errorMessage.style.display = 'block';
                }
            };

            reader.onerror = (error) => {
                console.error('Error reading file:', error);
                errorMessage.textContent = 'Error reading audio file. Please try again.';
                errorMessage.style.display = 'block';
            };

            reader.readAsArrayBuffer(file);
        });

        playPauseBtn.addEventListener('click', () => {
            if (isPlaying) {
                source.stop();
                isPlaying = false;
                cancelAnimationFrame(animationFrame);
                playPauseBtn.textContent = 'Play';
            } else {
                source = audioContext.createBufferSource();
                source.buffer = audioBuffer;
                source.connect(analyser);
                source.connect(audioContext.destination);
                source.start(0);
                isPlaying = true;
                function animate() {
                    drawVisualization();
                    animationFrame = requestAnimationFrame(animate);
                }
                animate();
                playPauseBtn.textContent = 'Pause';
                source.onended = () => {
                    isPlaying = false;
                    cancelAnimationFrame(animationFrame);
                    playPauseBtn.textContent = 'Play';
                };
            }
        });

        generateBtn.addEventListener('click', generateVideo);
    </script>
</body>
</html>
