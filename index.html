document.addEventListener('DOMContentLoaded', () => {
    // --- DOM Elements ---
    const loadingScreen = document.getElementById('loading-screen');
    const gameArea = document.getElementById('game-area');
    const sequenceDisplay = document.getElementById('sequence-display');
    const answerInput = document.getElementById('answer-input');
    const submitButton = document.getElementById('submit-button');
    const feedbackArea = document.getElementById('feedback-area');
    const explanationArea = document.getElementById('explanation-area');
    const explanationTitle = document.getElementById('explanation-title');
    const explanationFullSequence = document.getElementById('explanation-full-sequence');
    const oeisLink = document.getElementById('oeis-link');
    const nextQuestionButton = document.getElementById('next-question-button');
    const errorArea = document.getElementById('error-area');
    const errorMessage = document.getElementById('error-message');
    const retryButton = document.getElementById('retry-button');

    // --- Game State ---
    let currentSequenceData = null;
    let termsToDisplay = 5; // 表示する項の数
    let answer = null;

    // --- Pre-selected OEIS IDs ---
    // 有名で、比較的パターンが推測しやすく、ゲームに適していると思われる数列
    // 例: A000045 (フィボナッチ), A000027 (自然数), A000290 (平方数), A000217 (三角数),
    // A005843 (偶数), A000004 (ゼロの列 - これは簡単すぎるので注意), A000012 (1の列)
    // A000040 (素数), A000124 (中心つき多角数)
    let oeisIdPool = ["A000045", "A000027", "A000290", "A000217", "A005843", "A000040", "A000124", "A000032", "A000079"];
    let usedOeisIds = [];


    // --- API Fetch Function ---
    async function fetchOEISSequence(oeisId) {
        showLoading();
        try {
            // OEISは通常、数秒以内のリクエスト間隔を許容しますが、プロキシの必要性は状況によります。
            // 直接APIを叩きます。
            const response = await fetch(`https://oeis.org/search?q=id:${oeisId}&fmt=json`);
            if (!response.ok) {
                throw new Error(`OEIS API error: ${response.status} ${response.statusText}`);
            }
            const data = await response.json();

            if (data.results && data.results.length > 0) {
                const sequenceInfo = data.results[0];
                const numbersString = sequenceInfo.data;
                const name = sequenceInfo.name || `OEIS Sequence ${oeisId}`; // 名前がない場合

                if (!numbersString) {
                  throw new Error(`Sequence data not found for ${oeisId}.`);
                }

                const numbers = numbersString.split(',').map(Number);

                // ゲームに必要な最小限の項数があるか確認
                if (numbers.length < termsToDisplay + 1) {
                    throw new Error(`Sequence ${oeisId} is too short for the game (${numbers.length} terms).`);
                }
                return {
                    id: oeisId,
                    name: name,
                    numbers: numbers
                };
            } else {
                throw new Error(`Sequence ${oeisId} not found or no results.`);
            }
        } catch (error) {
            console.error("Failed to fetch OEIS sequence:", error);
            showError(`数列データの取得に失敗しました: ${error.message}`);
            return null;
        } finally {
            hideLoading();
        }
    }

    // --- UI Update Functions ---
    function showLoading() {
        loadingScreen.classList.remove('hidden');
        loadingScreen.classList.add('active');
        gameArea.classList.add('hidden');
        errorArea.classList.add('hidden');
    }

    function hideLoading() {
        loadingScreen.classList.add('hidden');
        loadingScreen.classList.remove('active');
    }

    function showError(message) {
        hideLoading();
        gameArea.classList.add('hidden');
        errorMessage.textContent = message;
        errorArea.classList.remove('hidden');
    }


    function displayQuestion() {
        gameArea.classList.remove('hidden');
        errorArea.classList.add('hidden');
        feedbackArea.classList.add('hidden');
        explanationArea.classList.add('hidden');
        nextQuestionButton.classList.add('hidden');
        answerInput.disabled = false;
        submitButton.disabled = false;
        answerInput.value = '';
        answerInput.focus();

        const sequenceToShow = currentSequenceData.numbers.slice(0, termsToDisplay);
        answer = currentSequenceData.numbers[termsToDisplay];

        sequenceDisplay.innerHTML = sequenceToShow.map(num => `<span>${num}</span>`).join(', ') + ', <span class="blank">__</span>';
    }

    // --- Game Logic ---
    async function setupNewQuestion() {
        if (oeisIdPool.length === 0) {
            showError("全ての数列を使い切りました！遊んでくれてありがとう！");
            answerInput.disabled = true;
            submitButton.disabled = true;
            retryButton.classList.add('hidden'); // 再試行ボタンも隠す
            return;
        }

        const randomIndex = Math.floor(Math.random() * oeisIdPool.length);
        const selectedId = oeisIdPool.splice(randomIndex, 1)[0];
        usedOeisIds.push(selectedId);

        currentSequenceData = await fetchOEISSequence(selectedId);

        if (currentSequenceData) {
            displayQuestion();
        } else {
            // fetchOEISSequence内でエラー表示されるので、ここでは何もしないか、
            // プールにIDを戻して別のIDで再試行するロジックを追加することもできる
            if (oeisIdPool.length > 0) {
                console.log("Retrying with another sequence...");
                setTimeout(setupNewQuestion, 100); // 少し待って再試行
            }
        }
    }

    function handleSubmit() {
        if (!currentSequenceData || answer === null) return;

        const userAnswer = parseInt(answerInput.value, 10);
        answerInput.disabled = true;
        submitButton.disabled = true;

        feedbackArea.classList.remove('hidden', 'correct', 'incorrect');
        if (userAnswer === answer) {
            feedbackArea.textContent = '正解！素晴らしい！';
            feedbackArea.classList.add('correct');
        } else {
            feedbackArea.textContent = `残念！正解は ${answer} でした。`;
            feedbackArea.classList.add('incorrect');
        }

        explanationTitle.textContent = currentSequenceData.name;
        const fullDisplaySequence = currentSequenceData.numbers.slice(0, termsToDisplay + 1).join(', ');
        explanationFullSequence.textContent = `数列: ${fullDisplaySequence}, ...`;
        oeisLink.href = `https://oeis.org/${currentSequenceData.id}`;
        oeisLink.textContent = `OEISで ${currentSequenceData.id} を見る`;
        explanationArea.classList.remove('hidden');

        if (oeisIdPool.length > 0) {
            nextQuestionButton.classList.remove('hidden');
        } else {
            nextQuestionButton.classList.add('hidden');
            // Optionally, display a "Game Over" message more prominently
        }
    }


    // --- Event Listeners ---
    submitButton.addEventListener('click', handleSubmit);
    answerInput.addEventListener('keypress', (event) => {
        if (event.key === 'Enter') {
            handleSubmit();
        }
    });
    nextQuestionButton.addEventListener('click', setupNewQuestion);
    retryButton.addEventListener('click', () => {
        errorArea.classList.add('hidden'); // エラーメッセージを隠す
        // プールが空でなければIDを戻すか、あるいは単に新しい質問をセットアップする
        if (usedOeisIds.length > 0 && !oeisIdPool.includes(usedOeisIds[usedOeisIds.length -1])) {
            // 失敗したIDをプールに戻す（無限ループを避けるため、失敗したIDが既にプールにないことを確認）
            // oeisIdPool.push(usedOeisIds.pop());
        }
        setupNewQuestion();
    });

    // --- Initialize Game ---
    setupNewQuestion();
});
