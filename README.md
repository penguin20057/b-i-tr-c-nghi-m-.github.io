<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đề Thi Trắc Nghiệm: Nhân Ma Trận & Phương Trình Newton</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.2/es5/tex-mml-chtml.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.8.0/math.min.js"></script>
    <style>
        .mathjax {
            font-size: 1.2rem;
            margin: 10px 0;
        }
        canvas {
            max-width: 100%;
            height: auto;
        }
    </style>
</head>
<body class="bg-gray-100 font-sans">
    <div class="container mx-auto p-6 max-w-4xl">
        <h1 class="text-3xl font-bold text-center mb-8">Đề Thi Trắc Nghiệm: Nhân Ma Trận & Phương Trình Newton</h1>
        <div id="quiz" class="space-y-6"></div>
        <button id="submit" class="mt-6 bg-blue-500 text-white px-6 py-2 rounded hover:bg-blue-600">Nộp bài</button>
        <div id="result" class="mt-6 hidden">
            <h2 class="text-2xl font-semibold">Kết quả</h2>
            <p id="score" class="text-lg"></p>
            <div id="explanations" class="mt-4 space-y-4"></div>
        </div>
    </div>

    <script>
        const questions = [
            {
                id: 1,
                text: "Tính tích của hai ma trận: \\[ A = \\begin{bmatrix} 1 & 2 \\\\ 3 & 4 \\end{bmatrix}, B = \\begin{bmatrix} 5 & 6 \\\\ 7 & 8 \\end{bmatrix} \\]. Kết quả là:",
                options: [
                    "\\[ \\begin{bmatrix} 19 & 22 \\\\ 43 & 50 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 10 & 12 \\\\ 21 & 24 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 5 & 12 \\\\ 21 & 32 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 15 & 18 \\\\ 28 & 32 \\end{bmatrix} \\]"
                ],
                correct: 0,
                explanation: "Nhân ma trận \\( A \\times B \\): \\[ \\begin{bmatrix} 1 & 2 \\\\ 3 & 4 \\end{bmatrix} \\times \\begin{bmatrix} 5 & 6 \\\\ 7 & 8 \\end{bmatrix} = \\begin{bmatrix} 1 \\cdot 5 + 2 \\cdot 7 & 1 \\cdot 6 + 2 \\cdot 8 \\\\ 3 \\cdot 5 + 4 \\cdot 7 & 3 \\cdot 6 + 4 \\cdot 8 \\end{bmatrix} = \\begin{bmatrix} 19 & 22 \\\\ 43 & 50 \\end{bmatrix} \\]."
            },
            {
                id: 2,
                text: "Cho ma trận \\( A = \\begin{bmatrix} 0 & 1 \\\\ 1 & 0 \\end{bmatrix} \\) và \\( B = \\begin{bmatrix} 2 & 3 \\\\ 4 & 5 \\end{bmatrix} \\). Tích \\( A \\times B \\) là:",
                options: [
                    "\\[ \\begin{bmatrix} 4 & 5 \\\\ 2 & 3 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 2 & 3 \\\\ 4 & 5 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 0 & 1 \\\\ 2 & 3 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 1 & 1 \\\\ 1 & 1 \\end{bmatrix} \\]"
                ],
                correct: 0,
                explanation: "Nhân ma trận \\( A \\times B \\): \\[ \\begin{bmatrix} 0 & 1 \\\\ 1 & 0 \\end{bmatrix} \\times \\begin{bmatrix} 2 & 3 \\\\ 4 & 5 \\end{bmatrix} = \\begin{bmatrix} 0 \\cdot 2 + 1 \\cdot 4 & 0 \\cdot 3 + 1 \\cdot 5 \\\\ 1 \\cdot 2 + 0 \\cdot 4 & 1 \\cdot 3 + 0 \\cdot 5 \\end{bmatrix} = \\begin{bmatrix} 4 & 5 \\\\ 2 & 3 \\end{bmatrix} \\]."
            },
            {
                id: 3,
                text: "Ma trận \\( A = \\begin{bmatrix} 1 & 2 & 3 \\end{bmatrix} \\) nhân với \\( B = \\begin{bmatrix} 4 \\\\ 5 \\\\ 6 \\end{bmatrix} \\). Kết quả là:",
                options: [
                    "\\[ \\begin{bmatrix} 32 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 12 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 20 \\end{bmatrix} \\]",
                    "\\[ \\begin{bmatrix} 15 \\end{bmatrix} \\]"
                ],
                correct: 2,
                explanation: "Nhân ma trận \\( A \\times B \\): \\[ \\begin{bmatrix} 1 & 2 & 3 \\end{bmatrix} \\times \\begin{bmatrix} 4 \\\\ 5 \\\\ 6 \\end{bmatrix} = 1 \\cdot 4 + 2 \\cdot 5 + 3 \\cdot 6 = 4 + 10 + 18 = 20 \\]. Kết quả là ma trận \\( \\begin{bmatrix} 20 \\end{bmatrix} \\)."
            },
            {
                id: 4,
                text: "Một vật có khối lượng \\( m = 5 \\, \\text{kg} \\) chịu lực \\( F = 20 \\, \\text{N} \\). Gia tốc của vật theo phương trình Newton là:",
                options: [
                    "\\( 2 \\, \\text{m/s}^2 \\)",
                    "\\( 4 \\, \\text{m/s}^2 \\)",
                    "\\( 6 \\, \\text{m/s}^2 \\)",
                    "\\( 8 \\, \\text{m/s}^2 \\)"
                ],
                correct: 1,
                explanation: "Theo phương trình Newton: \\( F = m \\cdot a \\), suy ra \\( a = \\frac{F}{m} = \\frac{20}{5} = 4 \\, \\text{m/s}^2 \\)."
            },
            {
                id: 5,
                text: "Một vật có khối lượng \\( m = 10 \\, \\text{kg} \\) chuyển động với gia tốc \\( a = 3 \\, \\text{m/s}^2 \\). Lực tác dụng lên vật là bao nhiêu? (Biểu đồ lực-gia tốc được vẽ bên dưới)",
                options: [
                    "\\( 20 \\, \\text{N} \\)",
                    "\\( 30 \\, \\text{N} \\)",
                    "\\( 40 \\, \\text{N} \\)",
                    "\\( 50 \\, \\text{N} \\)"
                ],
                correct: 1,
                explanation: "Theo phương trình Newton: \\( F = m \\cdot a = 10 \\cdot 3 = 30 \\, \\text{N} \\)."
            }
        ];

        const quizContainer = document.getElementById('quiz');
        const submitButton = document.getElementById('submit');
        const resultContainer = document.getElementById('result');
        const scoreElement = document.getElementById('score');
        const explanationsContainer = document.getElementById('explanations');
        let userAnswers = {};

        // Hiển thị câu hỏi
        function renderQuiz() {
            quizContainer.innerHTML = '';
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'bg-white p-6 rounded-lg shadow-md';
                questionDiv.innerHTML = `
                    <h3 class="text-xl font-semibold mb-4">Câu ${q.id}: ${q.text}</h3>
                    <div class="mathjax">${q.options.join('<br>')}</div>
                    ${q.id === 5 ? '<canvas id="newtonChart" class="mt-4"></canvas>' : ''}
                    <div class="mt-4 space-y-2">
                        ${q.options.map((opt, i) => `
                            <label class="block">
                                <input type="radio" name="q${q.id}" value="${i}" class="mr-2">
                                ${opt}
                            </label>
                        `).join('')}
                    </div>
                `;
                quizContainer.appendChild(questionDiv);
            });
            MathJax.typeset();
            if (document.getElementById('newtonChart')) {
                drawNewtonChart();
            }
        }

        // Vẽ biểu đồ lực-gia tốc cho câu 5
        function drawNewtonChart() {
            const canvas = document.getElementById('newtonChart');
            const ctx = canvas.getContext('2d');
            canvas.width = 400;
            canvas.height = 200;

            // Vẽ lưới
            ctx.strokeStyle = '#ddd';
            ctx.lineWidth = 1;
            for (let x = 0; x <= 400; x += 40) {
                ctx.beginPath();
                ctx.moveTo(x, 0);
                ctx.lineTo(x, 200);
                ctx.stroke();
            }
            for (let y = 0; y <= 200; y += 20) {
                ctx.beginPath();
                ctx.moveTo(0, y);
                ctx.lineTo(400, y);
                ctx.stroke();
            }

            // Vẽ trục
            ctx.strokeStyle = '#000';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, 200);
            ctx.lineTo(400, 200);
            ctx.moveTo(0, 0);
            ctx.lineTo(0, 200);
            ctx.stroke();

            // Vẽ đường lực (F = 10 * a)
            ctx.strokeStyle = '#007bff';
            ctx.beginPath();
            ctx.moveTo(0, 200);
            for (let a = 0; a <= 10; a += 0.1) {
                const F = 10 * a;
                const x = a * 40;
                const y = 200 - (F * 4);
                ctx.lineTo(x, y);
            }
            ctx.stroke();

            // Ghi nhãn
            ctx.fillStyle = '#000';
            ctx.font = '12px Arial';
            ctx.fillText('Gia tốc (m/s²)', 350, 195);
            ctx.fillText('Lực (N)', 10, 10);
            for (let i = 0; i <= 10; i++) {
                ctx.fillText(i, i * 40, 215);
                ctx.fillText(i * 5, -20, 200 - i * 20);
            }
        }

        // Kiểm tra đáp án
        function checkAnswers() {
            let score = 0;
            const explanations = [];
            questions.forEach(q => {
                const selected = document.querySelector(`input[name="q${q.id}"]:checked`);
                const userAnswer = selected ? parseInt(selected.value) : -1;
                userAnswers[q.id] = userAnswer;
                if (userAnswer === q.correct) {
                    score++;
                }
                explanations.push(`
                    <div class="bg-gray-50 p-4 rounded">
                        <h3 class="font-semibold">Câu ${q.id}: ${userAnswer === q.correct ? 'Đúng' : 'Sai'}</h3>
                        <p>${q.explanation}</p>
                    </div>
                `);
            });
            scoreElement.textContent = `Bạn đúng ${score}/${questions.length} câu.`;
            explanationsContainer.innerHTML = explanations.join('');
            resultContainer.classList.remove('hidden');
            MathJax.typeset();
        }

        // Sự kiện nộp bài
        submitButton.addEventListener('click', checkAnswers);

        // Khởi tạo
        renderQuiz();
    </script>
</body>
</html>