<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мастер уравнений высших степеней</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        :root {
            --primary: #6366f1;
            --primary-dark: #4f46e5;
            --secondary: #10b981;
            --dark: #1e293b;
            --light: #f8fafc;
            --gray: #94a3b8;
            --danger: #ef4444;
            --warning: #f59e0b;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--light);
            color: var(--dark);
            min-height: 100vh;
            transition: all 0.3s ease;
        }
        
        .dark body {
            background-color: #0f172a;
            color: var(--light);
        }
        
        .neumorphism {
            background: var(--light);
            box-shadow: 8px 8px 16px #d1d9e6, -8px -8px 16px #ffffff;
            border-radius: 16px;
        }
        
        .dark .neumorphism {
            background: #1e293b;
            box-shadow: 8px 8px 16px #0f172a, -8px -8px 16px #334155;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            background: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .btn-secondary {
            background: var(--secondary);
            color: white;
            transition: all 0.3s ease;
        }
        
        .btn-secondary:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .math-icon {
            width: 48px;
            height: 48px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 12px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            font-size: 1.5rem;
        }
        
        .theme-switch {
            position: relative;
            width: 60px;
            height: 30px;
            border-radius: 15px;
            background: var(--gray);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .theme-switch::after {
            content: '';
            position: absolute;
            width: 26px;
            height: 26px;
            border-radius: 50%;
            background: white;
            top: 2px;
            left: 2px;
            transition: all 0.3s ease;
        }
        
        .dark .theme-switch {
            background: var(--primary);
        }
        
        .dark .theme-switch::after {
            left: 32px;
        }
        
        .floating {
            animation: floating 6s ease-in-out infinite;
        }
        
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .progress-bar {
            height: 8px;
            border-radius: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            transition: width 0.5s ease;
        }
        
        .task-card {
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .task-card:hover {
            transform: translateY(-5px);
            border-color: var(--primary);
        }
        
        .slide-in {
            animation: slideIn 0.5s forwards;
        }
        
        @keyframes slideIn {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        .fade-in {
            animation: fadeIn 0.5s forwards;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: var(--primary);
            opacity: 0;
            z-index: 9999;
            animation: confetti 3s ease-in-out forwards;
        }
        
        @keyframes confetti {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body class="antialiased">
    <!-- Главное меню -->
    <div id="main-menu" class="container mx-auto px-4 py-8">
        <!-- Хедер -->
        <header class="flex justify-between items-center mb-8">
            <div class="flex items-center">
                <div class="w-10 h-10 rounded-full bg-gradient-to-r from-purple-500 to-indigo-600 flex items-center justify-center text-white mr-3">
                    <i class="fas fa-square-root-alt"></i>
                </div>
                <h1 class="text-xl font-bold">MathMaster</h1>
            </div>
            <div class="flex items-center space-x-4">
                <div class="flex items-center">
                    <span class="mr-2 text-sm hidden sm:inline"><i class="fas fa-moon"></i></span>
                    <div class="theme-switch" onclick="toggleDarkMode()"></div>
                    <span class="ml-2 text-sm hidden sm:inline"><i class="fas fa-sun"></i></span>
                </div>
                <button onclick="showSettings()" class="w-10 h-10 rounded-full bg-gray-200 dark:bg-slate-700 flex items-center justify-center">
                    <i class="fas fa-cog"></i>
                </button>
            </div>
        </header>
        
        <!-- Герой секция -->
        <div class="floating mb-12 text-center">
            <h1 class="text-4xl md:text-5xl font-bold mb-4 bg-gradient-to-r from-purple-600 to-indigo-600 bg-clip-text text-transparent">
                Мастер уравнений
            </h1>
            <p class="text-lg text-gray-600 dark:text-gray-300 max-w-2xl mx-auto">
                Совершенствуйте навыки решения уравнений высших степеней с интерактивными заданиями и мгновенной обратной связью
            </p>
        </div>
        
        <!-- Карточка с кнопками -->
        <div class="neumorphism p-6 md:p-8 mb-12 max-w-4xl mx-auto">
            <!-- Кнопка теории -->
            <button onclick="showTheory()" class="btn-primary text-white font-bold py-4 px-8 rounded-xl mb-8 w-full max-w-md mx-auto flex items-center justify-center">
                <i class="fas fa-book-open mr-3"></i> Теоретический материал
            </button>
            
            <h2 class="text-2xl font-semibold mb-6 text-center">Практические блоки</h2>
            
            <!-- Блоки задач -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                <button onclick="startBlock(1)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-square-root-alt"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Виды уравнений</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Изучите различные типы уравнений высших степеней</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
                
                <button onclick="startBlock(2)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-layer-group"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Решение по ФСУ</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Применение формул сокращенного умножения</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
                
                <button onclick="startBlock(3)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-function"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Метод группировки</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Группировка слагаемых для упрощения</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
                
                <button onclick="startBlock(4)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-table"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Схема Горнера</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Эффективное деление многочленов</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
                
                <button onclick="startBlock(5)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-exchange-alt"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Теорема Безу</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Поиск корней среди делителей</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
                
                <button onclick="startBlock(6)" class="task-card neumorphism p-6 text-left group">
                    <div class="flex items-center mb-3">
                        <div class="math-icon mr-4">
                            <i class="fas fa-superscript"></i>
                        </div>
                        <h3 class="text-lg font-semibold">Новая переменная</h3>
                    </div>
                    <p class="text-gray-500 dark:text-gray-400 text-sm">Упрощение уравнений заменой</p>
                    <div class="mt-4 flex justify-between items-center">
                        <span class="text-xs px-2 py-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 rounded-full">12 заданий</span>
                        <i class="fas fa-chevron-right text-gray-400 group-hover:text-indigo-500"></i>
                    </div>
                </button>
            </div>
        </div>
        
        <!-- Футер -->
        <footer class="text-center text-gray-500 dark:text-gray-400 text-sm mt-12">
            <p>© 2023 MathMaster. Все права защищены.</p>
        </footer>
    </div>
    
    <!-- Теоретический блок (скрыт по умолчанию) -->
    <div id="theory-section" class="hidden container mx-auto px-4 py-8 max-w-4xl">
        <button onclick="showMainMenu()" class="flex items-center text-gray-500 dark:text-gray-400 hover:text-indigo-600 dark:hover:text-indigo-400 mb-8">
            <i class="fas fa-arrow-left mr-2"></i> Назад
        </button>
        
        <div class="neumorphism rounded-2xl p-6 md:p-8">
            <h2 class="text-3xl font-bold mb-6 bg-gradient-to-r from-blue-500 to-blue-600 bg-clip-text text-transparent">
                Теоретический материал
            </h2>
            
            <div class="prose dark:prose-invert max-w-none">
                <div class="flex items-center mb-6">
                    <div class="w-12 h-12 rounded-lg bg-gradient-to-r from-blue-500 to-blue-600 flex items-center justify-center text-white mr-4">
                        <i class="fas fa-info-circle text-xl"></i>
                    </div>
                    <h3 class="text-xl font-semibold">Решение уравнений высших степеней</h3>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-blue-50 dark:bg-blue-900/30 p-5 rounded-xl">
                        <h4 class="font-semibold text-blue-600 dark:text-blue-400 mb-3 flex items-center">
                            <i class="fas fa-cube mr-2"></i> Основные понятия
                        </h4>
                        <p class="text-sm">Уравнение высшей степени - это уравнение вида:</p>
                        <div class="text-center my-3 font-mono bg-blue-100 dark:bg-blue-900 p-3 rounded-lg text-blue-800 dark:text-blue-200">
                            P(x) = 0, где P(x) — многочлен степени n ≥ 3
                        </div>
                        <p class="text-sm">Примеры: x³ - 6x² + 11x - 6 = 0 (кубическое), x⁴ - 5x² + 4 = 0 (биквадратное).</p>
                    </div>
                    
                    <div class="bg-green-50 dark:bg-green-900/30 p-5 rounded-xl">
                        <h4 class="font-semibold text-green-600 dark:text-green-400 mb-3 flex items-center">
                            <i class="fas fa-lightbulb mr-2"></i> Общий подход
                        </h4>
                        <ol class="list-decimal list-inside text-sm space-y-2">
                            <li>Попробовать разложить на множители</li>
                            <li>Искать рациональные корни</li>
                            <li>Применить замену переменной</li>
                            <li>Использовать графический метод</li>
                        </ol>
                    </div>
                </div>
                
                <h4 class="font-semibold text-lg mb-4 mt-8">Методы решения</h4>
                
                <div class="space-y-4">
                    <div class="p-5 bg-white dark:bg-slate-800 rounded-xl border-l-4 border-blue-500">
                        <h5 class="font-semibold text-blue-600 dark:text-blue-400 flex items-center">
                            <i class="fas fa-calculator mr-2"></i> Разложение на множители
                        </h5>
                        <p class="text-sm mt-2">Ищите общие множители или используйте формулы сокращенного умножения.</p>
                        <div class="mt-3 bg-gray-100 dark:bg-slate-700 p-3 rounded-lg text-sm">
                            <p class="font-mono">x³ - x² - 4x + 4 = 0</p>
                            <p class="font-mono">x²(x - 1) - 4(x - 1) = 0</p>
                            <p class="font-mono">(x - 1)(x² - 4) = 0</p>
                        </div>
                    </div>
                    
                    <div class="p-5 bg-white dark:bg-slate-800 rounded-xl border-l-4 border-purple-500">
                        <h5 class="font-semibold text-purple-600 dark:text-purple-400 flex items-center">
                            <i class="fas fa-project-diagram mr-2"></i> Метод группировки
                        </h5>
                        <p class="text-sm mt-2">Группируйте слагаемые так, чтобы можно было вынести общий множитель.</p>
                        <div class="mt-3 bg-gray-100 dark:bg-slate-700 p-3 rounded-lg text-sm">
                            <p class="font-mono">x³ + 3x² - 4x - 12 = 0</p>
                            <p class="font-mono">x²(x + 3) - 4(x + 3) = 0</p>
                            <p class="font-mono">(x + 3)(x² - 4) = 0</p>
                        </div>
                    </div>
                    
                    <div class="p-5 bg-white dark:bg-slate-800 rounded-xl border-l-4 border-indigo-500">
                        <h5 class="font-semibold text-indigo-600 dark:text-indigo-400 flex items-center">
                            <i class="fas fa-table mr-2"></i> Схема Горнера
                        </h5>
                        <p class="text-sm mt-2">Позволяет делить многочлен на (x - c) и находить корни.</p>
                        <div class="mt-3 bg-gray-100 dark:bg-slate-700 p-3 rounded-lg text-sm">
                            <p class="font-mono">Для P(x) = 2x³ - 5x² - 4x + 3, x=3:</p>
                            <p class="font-mono">2 | -5 | -4 | 3</p>
                            <p class="font-mono">3→ 6 | 3 | -3</p>
                            <p class="font-mono">2 | 1 | -1 | 0 ← корень</p>
                        </div>
                    </div>
                    
                    <div class="p-5 bg-white dark:bg-slate-800 rounded-xl border-l-4 border-green-500">
                        <h5 class="font-semibold text-green-600 dark:text-green-400 flex items-center">
                            <i class="fas fa-bezier-curve mr-2"></i> Теорема Безу
                        </h5>
                        <p class="text-sm mt-2">Если a — корень, то P(x) делится на (x - a) без остатка.</p>
                        <div class="mt-3 bg-gray-100 dark:bg-slate-700 p-3 rounded-lg text-sm">
                            <p class="font-mono">Для P(x) = x³ - 6x² + 11x - 6</p>
                            <p class="font-mono">Пробуем x=1: 1 - 6 + 11 - 6 = 0 → корень</p>
                            <p class="font-mono">Делим на (x - 1): x² - 5x + 6 = 0</p>
                        </div>
                    </div>
                    
                    <div class="p-5 bg-white dark:bg-slate-800 rounded-xl border-l-4 border-red-500">
                        <h5 class="font-semibold text-red-600 dark:text-red-400 flex items-center">
                            <i class="fas fa-exchange-alt mr-2"></i> Метод замены
                        </h5>
                        <p class="text-sm mt-2">Заменяйте часть уравнения новой переменной (например, x² = t).</p>
                        <div class="mt-3 bg-gray-100 dark:bg-slate-700 p-3 rounded-lg text-sm">
                            <p class="font-mono">x⁴ - 5x² + 4 = 0</p>
                            <p class="font-mono">Пусть x² = t: t² - 5t + 4 = 0</p>
                            <p class="font-mono">Решаем: t=1, t=4 → x=±1, x=±2</p>
                        </div>
                    </div>
                </div>
                
                <div class="mt-8 p-5 bg-indigo-50 dark:bg-indigo-900/30 rounded-xl">
                    <h4 class="font-semibold text-indigo-600 dark:text-indigo-400 mb-3 flex items-center">
                        <i class="fas fa-graduation-cap mr-2"></i> Пример решения
                    </h4>
                    <p class="text-sm">Уравнение: x³ - 6x² + 11x - 6 = 0</p>
                    <ol class="list-decimal list-inside text-sm space-y-2 mt-2">
                        <li>По теореме Безу: x = 1 — корень.</li>
                        <li>Делим многочлен на (x - 1): получаем x² - 5x + 6 = 0.</li>
                        <li>Решаем квадратное уравнение: x = 2, x = 3.</li>
                    </ol>
                    <div class="mt-3 font-bold text-indigo-800 dark:text-indigo-200">
                        Ответ: x ∈ {1, 2, 3}.
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Блок с задачей (скрыт по умолчанию) -->
    <div id="problem-section" class="hidden container mx-auto px-4 py-8 max-w-2xl">
        <button onclick="showMainMenu()" class="flex items-center text-gray-500 dark:text-gray-400 hover:text-indigo-600 dark:hover:text-indigo-400 mb-8">
            <i class="fas fa-arrow-left mr-2"></i> Назад
        </button>
        
        <div class="neumorphism rounded-2xl p-6 md:p-8 slide-in">
            <!-- Заголовок блока -->
            <div class="flex justify-between items-center mb-6">
                <div>
                    <h2 id="block-title" class="text-xl font-bold text-indigo-600 dark:text-indigo-400"></h2>
                    <p class="text-sm text-gray-500 dark:text-gray-400">Практическое задание</p>
                </div>
                <div class="flex items-center space-x-3">
                    <span id="problem-counter" class="bg-indigo-100 dark:bg-indigo-900 text-indigo-800 dark:text-indigo-200 px-3 py-1 rounded-full text-sm"></span>
                    <span id="score-counter" class="bg-green-100 dark:bg-green-900 text-green-800 dark:text-green-200 px-3 py-1 rounded-full text-sm"></span>
                </div>
            </div>
            
            <!-- Прогресс бар -->
            <div class="w-full bg-gray-200 dark:bg-slate-700 rounded-full h-2 mb-6">
                <div id="progress-bar" class="progress-bar h-2 rounded-full"></div>
            </div>
            
            <!-- Текст задачи -->
            <div class="neumorphism-inner bg-gray-50 dark:bg-slate-800 rounded-xl p-6 mb-6">
                <div class="flex items-center mb-4">
                    <div class="w-10 h-10 rounded-lg bg-indigo-100 dark:bg-indigo-900 flex items-center justify-center text-indigo-600 dark:text-indigo-400 mr-3">
                        <i class="fas fa-question"></i>
                    </div>
                    <h3 class="font-medium">Решите уравнение:</h3>
                </div>
                <p id="problem-text" class="text-lg font-mono text-center py-4"></p>
            </div>
            
            <!-- Поле для ответа -->
            <div class="mb-6">
                <label for="answer-input" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Ваш ответ:</label>
                <div class="relative">
                    <input type="text" id="answer-input" class="w-full px-4 py-3 bg-white dark:bg-slate-800 border border-gray-300 dark:border-slate-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 text-gray-900 dark:text-white placeholder-gray-400 dark:placeholder-gray-500" placeholder="Введите корни уравнения...">
                    <button onclick="showKeyboard()" class="absolute right-3 top-3 text-gray-400 hover:text-indigo-500">
                        <i class="fas fa-keyboard"></i>
                    </button>
                </div>
                <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">Для нескольких корней разделяйте их запятыми (например: 1, -2, 3.5)</p>
            </div>
            
            <!-- Кнопки -->
            <div class="flex flex-col sm:flex-row gap-3">
                <button onclick="checkAnswer()" class="btn-primary text-white font-bold py-3 px-6 rounded-lg flex-1 flex items-center justify-center">
                    <i class="fas fa-check-circle mr-2"></i> Проверить
                </button>
                <button onclick="showHint()" class="bg-gray-200 dark:bg-slate-700 hover:bg-gray-300 dark:hover:bg-slate-600 text-gray-800 dark:text-gray-200 font-bold py-3 px-6 rounded-lg flex-1 flex items-center justify-center">
                    <i class="fas fa-lightbulb mr-2"></i> Подсказка
                </button>
                <button onclick="skipProblem()" class="bg-gray-100 dark:bg-slate-800 hover:bg-gray-200 dark:hover:bg-slate-700 text-gray-600 dark:text-gray-400 font-bold py-3 px-6 rounded-lg flex-1 flex items-center justify-center">
                    <i class="fas fa-forward mr-2"></i> Пропустить
                </button>
            </div>
        </div>
    </div>
    
    <!-- Результаты (скрыт по умолчанию) -->
    <div id="results-section" class="hidden container mx-auto px-4 py-8 max-w-md">
        <div class="neumorphism rounded-2xl p-8 text-center fade-in">
            <div class="p-6">
                <div id="result-icon" class="w-24 h-24 rounded-full bg-gradient-to-r from-indigo-500 to-purple-600 flex items-center justify-center text-white text-4xl mx-auto mb-6"></div>
                <h2 id="result-title" class="text-3xl font-bold mb-4"></h2>
                <p id="result-score" class="text-xl mb-2"></p>
                <div class="w-full bg-gray-200 dark:bg-slate-700 rounded-full h-3 mb-6">
                    <div id="result-progress" class="h-3 rounded-full"></div>
                </div>
                <p id="result-message" class="text-lg mb-8"></p>
                
                <div class="grid grid-cols-1 gap-3">
                    <button onclick="retryBlock()" class="btn-primary text-white font-bold py-3 px-6 rounded-lg">
                        <i class="fas fa-redo mr-2"></i> Попробовать еще раз
                    </button>
                    <button onclick="showMainMenu()" class="bg-gray-200 dark:bg-slate-700 hover:bg-gray-300 dark:hover:bg-slate-600 text-gray-800 dark:text-gray-200 font-bold py-3 px-6 rounded-lg">
                        <i class="fas fa-home mr-2"></i> В главное меню
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Подсказка (модальное окно) -->
    <div id="hint-modal" class="hidden fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 px-4">
        <div class="neumorphism rounded-2xl p-6 max-w-md w-full slide-in">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-bold text-indigo-600 dark:text-indigo-400 flex items-center">
                    <i class="fas fa-lightbulb mr-2"></i> Подсказка
                </h3>
                <button onclick="closeHint()" class="text-gray-400 hover:text-indigo-500">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="bg-indigo-50 dark:bg-indigo-900/20 p-4 rounded-lg mb-4">
                <p id="hint-text" class="text-gray-700 dark:text-gray-300"></p>
            </div>
            <button onclick="closeHint()" class="btn-primary text-white font-bold py-2 px-4 rounded-lg w-full">
                Понятно
            </button>
        </div>
    </div>
    
    <!-- Настройки (модальное окно) -->
    <div id="settings-modal" class="hidden fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 px-4">
        <div class="neumorphism rounded-2xl p-6 max-w-md w-full slide-in">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-bold text-indigo-600 dark:text-indigo-400 flex items-center">
                    <i class="fas fa-cog mr-2"></i> Настройки
                </h3>
                <button onclick="closeSettings()" class="text-gray-400 hover:text-indigo-500">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Тема интерфейса</label>
                    <div class="flex items-center space-x-4">
                        <button onclick="setLightTheme()" class="flex-1 py-2 px-4 rounded-lg border-2 border-gray-300 dark:border-slate-600 flex items-center justify-center">
                            <i class="fas fa-sun mr-2"></i> Светлая
                        </button>
                        <button onclick="setDarkTheme()" class="flex-1 py-2 px-4 rounded-lg border-2 border-gray-300 dark:border-slate-600 flex items-center justify-center">
                            <i class="fas fa-moon mr-2"></i> Темная
                        </button>
                    </div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Количество заданий</label>
                    <select id="task-count" class="w-full px-4 py-2 bg-white dark:bg-slate-800 border border-gray-300 dark:border-slate-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 text-gray-900 dark:text-white">
                        <option value="5">5 заданий</option>
                        <option value="10" selected>10 заданий</option>
                        <option value="15">15 заданий</option>
                        <option value="20">20 заданий</option>
                    </select>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Уровень сложности</label>
                    <select id="difficulty" class="w-full px-4 py-2 bg-white dark:bg-slate-800 border border-gray-300 dark:border-slate-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 text-gray-900 dark:text-white">
                        <option value="easy">Легкий</option>
                        <option value="medium" selected>Средний</option>
                        <option value="hard">Сложный</option>
                    </select>
                </div>
            </div>
            
            <div class="mt-6 flex space-x-3">
                <button onclick="saveSettings()" class="btn-primary text-white font-bold py-2 px-4 rounded-lg flex-1">
                    Сохранить
                </button>
                <button onclick="closeSettings()" class="bg-gray-200 dark:bg-slate-700 hover:bg-gray-300 dark:hover:bg-slate-600 text-gray-800 dark:text-gray-200 font-bold py-2 px-4 rounded-lg flex-1">
                    Отмена
                </button>
            </div>
        </div>
    </div>
    
    <!-- Виртуальная клавиатура (модальное окно) -->
    <div id="keyboard-modal" class="hidden fixed inset-0 bg-black bg-opacity-70 flex items-end justify-center z-50 px-4 pb-4">
        <div class="neumorphism rounded-2xl p-4 w-full max-w-md slide-in">
            <div class="flex justify-between items-center mb-3">
                <h3 class="text-lg font-bold text-indigo-600 dark:text-indigo-400">Виртуальная клавиатура</h3>
                <button onclick="closeKeyboard()" class="text-gray-400 hover:text-indigo-500">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="grid grid-cols-6 gap-2 mb-2">
                <button onclick="insertSymbol('1')" class="keyboard-key">1</button>
                <button onclick="insertSymbol('2')" class="keyboard-key">2</button>
                <button onclick="insertSymbol('3')" class="keyboard-key">3</button>
                <button onclick="insertSymbol('4')" class="keyboard-key">4</button>
                <button onclick="insertSymbol('5')" class="keyboard-key">5</button>
                <button onclick="insertSymbol('6')" class="keyboard-key">6</button>
                <button onclick="insertSymbol('7')" class="keyboard-key">7</button>
                <button onclick="insertSymbol('8')" class="keyboard-key">8</button>
                <button onclick="insertSymbol('9')" class="keyboard-key">9</button>
                <button onclick="insertSymbol('0')" class="keyboard-key">0</button>
                <button onclick="insertSymbol('-')" class="keyboard-key">-</button>
                <button onclick="insertSymbol(',')" class="keyboard-key">,</button>
            </div>
            
            <div class="flex space-x-2">
                <button onclick="backspace()" class="keyboard-key flex-1">
                    <i class="fas fa-backspace"></i>
                </button>
                <button onclick="closeKeyboard()" class="keyboard-key flex-1 bg-indigo-100 dark:bg-indigo-900 text-indigo-600 dark:text-indigo-300">
                    Готово
                </button>
            </div>
        </div>
    </div>
    
    <script>
        // Текущее состояние приложения
        const appState = {
            currentBlock: 0,
            currentProblem: 0,
            score: 0,
            problems: [],
            settings: {
                theme: 'system',
                taskCount: 10,
                difficulty: 'medium'
            },
            blockNames: {
                1: "Виды уравнений",
                2: "Решение по ФСУ",
                3: "Метод группировки",
                4: "Схема Горнера",
                5: "Теорема Безу",
                6: "Новая переменная"
            },
            hints: {
                1: "Попробуйте разложить на множители или использовать подстановку. Для кубических уравнений ищите целые корни среди делителей свободного члена.",
                2: "Вспомните формулы разности квадратов (a² - b² = (a-b)(a+b)), разности кубов (a³ - b³ = (a-b)(a² + ab + b²)) и квадрата суммы/разности (a±b)² = a² ± 2ab + b².",
                3: "Сгруппируйте слагаемые так, чтобы можно было вынести общий множитель. Обычно группируют по два слагаемых, но иногда эффективнее другая группировка.",
                4: "Ищите целые корни среди делителей свободного члена. Для x=3 коэффициенты: 3 | a | b | c → a | (3a+b) | (3(3a+b)+c). Если последнее число 0 - это корень.",
                5: "Пробуйте подставлять делители свободного члена в уравнение. Если P(a)=0, то (x-a) - множитель многочлена. Затем делите многочлен на (x-a).",
                6: "Попробуйте заменить часть уравнения новой переменной (например, x² = t). Особенно эффективно для биквадратных уравнений и уравнений с повторяющимися выражениями."
            }
        };
        
        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            loadSettings();
            applyTheme();
            
            // Проверяем prefers-color-scheme
            if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
                if (appState.settings.theme === 'system') {
                    document.documentElement.classList.add('dark');
                }
            }
            
            // Слушаем изменения темы системы
            window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', e => {
                if (appState.settings.theme === 'system') {
                    if (e.matches) {
                        document.documentElement.classList.add('dark');
                    } else {
                        document.documentElement.classList.remove('dark');
                    }
                }
            });
        });
        
        // Показать главное меню
        function showMainMenu() {
            document.getElementById('main-menu').classList.remove('hidden');
            document.getElementById('theory-section').classList.add('hidden');
            document.getElementById('problem-section').classList.add('hidden');
            document.getElementById('results-section').classList.add('hidden');
        }
        
        // Показать теорию
        function showTheory() {
            document.getElementById('main-menu').classList.add('hidden');
            document.getElementById('theory-section').classList.remove('hidden');
        }
        
        // Начать блок задач
        function startBlock(blockNum) {
            appState.currentBlock = blockNum;
            appState.currentProblem = 0;
            appState.score = 0;
            appState.problems = generateProblems(blockNum, appState.settings.difficulty, appState.settings.taskCount);
            
            showProblem();
        }
        
        // Генерация задач
        function generateProblems(blockNum, difficulty, count) {
            const problems = [];
            const countInt = parseInt(count) || 10;
            
            for (let i = 0; i < countInt; i++) {
                let question, answer;
                let complexity = 1;
                
                if (difficulty === 'easy') complexity = 1;
                else if (difficulty === 'hard') complexity = 3;
                else complexity = 2; // medium
                
                switch (blockNum) {
                    case 1: // Виды уравнений
                        const eqType = Math.floor(Math.random() * 3) + 1;
                        if (eqType === 1) { // Кубическое уравнение
                            const roots = [
                                randomInt(-3 * complexity, 3 * complexity),
                                randomInt(-3 * complexity, 3 * complexity),
                                randomInt(-3 * complexity, 3 * complexity)
                            ].sort((a, b) => a - b);
                            question = `x³ ${roots.reduce((a,b)=>a+b,0) >= 0 ? '+' : ''}${-roots.reduce((a,b)=>a+b,0)}x² ${roots[0]*roots[1]+roots[0]*roots[2]+roots[1]*roots[2] >= 0 ? '+' : ''}${-roots[0]*roots[1]-roots[0]*roots[2]-roots[1]*roots[2]}x ${-roots[0]*roots[1]*roots[2] >= 0 ? '+' : ''}${roots[0]*roots[1]*roots[2]} = 0`;
                            answer = roots;
                        } else if (eqType === 2) { // Биквадратное уравнение
                            const b = [1, 4, 9, 16][Math.floor(Math.random() * 4)] * complexity;
                            const c = randomInt(0, 2) ? 0 : randomInt(1, 4) * complexity;
                            question = `x⁴ ${-b >= 0 ? '+' : ''}${-b}x² ${c ? (c >= 0 ? '+' : '') + c : ''} = 0`;
                            answer = c ? [-Math.sqrt((b + Math.sqrt(b*b - 4*c))/2), -Math.sqrt((b - Math.sqrt(b*b - 4*c))/2), Math.sqrt((b - Math.sqrt(b*b - 4*c))/2), Math.sqrt((b + Math.sqrt(b*b - 4*c))/2)].filter(x => !isNaN(x)).map(x => Math.round(x*100)/100) : [-Math.sqrt(b), 0, Math.sqrt(b)].map(x => Math.round(x));
                        } else { // Уравнение с кратными корнями
                            const root = randomInt(-2 * complexity, 2 * complexity);
                            const power = randomInt(2, 3);
                            question = `(x ${-root >= 0 ? '+' : ''}${-root})^${power} = 0`;
                            answer = Array(power).fill(root);
                        }
                        break;
                        
                    case 2: // Решение по ФСУ
                        const fsuType = Math.floor(Math.random() * 3) + 1;
                        if (fsuType === 1) { // Разность квадратов
                            const a = randomInt(1, 3 * complexity);
                            const b = randomInt(0, 2) ? 0 : randomInt(1, 2 * complexity);
                            question = `x² ${-a*a >= 0 ? '+' : ''}${-a*a} ${b ? (b >= 0 ? '+' : '') + b : ''} = 0`;
                            answer = b ? [-Math.sqrt(a*a - b), Math.sqrt(a*a - b)].filter(x => !isNaN(x)).map(x => Math.round(x*100)/100) : [-a, a];
                        } else if (fsuType === 2) { // Разность кубов
                            const a = randomInt(1, 2 * complexity);
                            question = `x³ ${-a*a*a >= 0 ? '+' : ''}${-a*a*a} = 0`;
                            answer = [a];
                        } else { // Квадрат суммы/разности
                            const a = randomInt(1, 2 * complexity);
                            const b = randomInt(1, 2 * complexity);
                            if (Math.random() > 0.5) {
                                question = `x² ${2*a*b >= 0 ? '+' : ''}${2*a*b}x ${a*b*a*b >= 0 ? '+' : ''}${a*b*a*b} = 0`;
                                answer = [-a*b];
                            } else {
                                question = `x² ${-2*a*b >= 0 ? '+' : ''}${-2*a*b}x ${a*b*a*b >= 0 ? '+' : ''}${a*b*a*b} = 0`;
                                answer = [a*b];
                            }
                        }
                        break;
                        
                    case 3: // Метод группировки
                        const roots = [
                            randomInt(-3 * complexity, 3 * complexity),
                            randomInt(-3 * complexity, 3 * complexity),
                            randomInt(-3 * complexity, 3 * complexity)
                        ].sort((a, b) => a - b);
                        const sum = roots[0] + roots[1] + roots[2];
                        const sumPairs = roots[0]*roots[1] + roots[0]*roots[2] + roots[1]*roots[2];
                        const product = roots[0] * roots[1] * roots[2];
                        question = `x³ ${-sum >= 0 ? '+' : ''}${-sum}x² ${sumPairs >= 0 ? '+' : ''}${sumPairs}x ${-product >= 0 ? '+' : ''}${-product} = 0`;
                        answer = roots;
                        break;
                        
                    case 4: // Схема Горнера
                        const root = randomInt(-3 * complexity, 3 * complexity);
                        const a = randomInt(1, 2 * complexity);
                        const b = randomInt(-5 * complexity, 5 * complexity);
                        const c = -root * b;
                        question = `${a}x³ ${b - a*root >= 0 ? '+' : ''}${b - a*root}x² ${c - b*root >= 0 ? '+' : ''}${c - b*root}x ${-c*root >= 0 ? '+' : ''}${-c*root} = 0`;
                        answer = [root, -Math.floor(c/b)].sort((x, y) => x - y);
                        break;
                        
                    case 5: // Теорема Безу
                        const possibleRoots = [-3, -2, -1, 1, 2, 3].map(x => x * complexity);
                        const selectedRoots = [];
                        const numRoots = randomInt(1, 3);
                        for (let j = 0; j < numRoots; j++) {
                            const idx = Math.floor(Math.random() * possibleRoots.length);
                            selectedRoots.push(possibleRoots[idx]);
                            possibleRoots.splice(idx, 1);
                        }
                        question = selectedRoots.map(r => `(x ${-r >= 0 ? '+' : ''}${-r})`).join(' * ') + ' = 0';
                        answer = selectedRoots.sort((x, y) => x - y);
                        break;
                        
                    case 6: // Новая переменная
                        const subType = Math.floor(Math.random() * 2) + 1;
                        if (subType === 1) { // Биквадратное
                            const b = [1, 4, 9, 16][Math.floor(Math.random() * 4)] * complexity;
                            question = `x⁴ ${-b >= 0 ? '+' : ''}${-b}x² = 0`;
                            answer = [-Math.sqrt(b), 0, Math.sqrt(b)].map(x => Math.round(x));
                        } else { // Уравнение вида x(x² + kx + m) = 0
                            const k = randomInt(1, 3 * complexity);
                            const m = randomInt(1, 3 * complexity);
                            question = `x³ ${k >= 0 ? '+' : ''}${k}x² ${m >= 0 ? '+' : ''}${m}x = 0`;
                            const discriminant = k*k - 4*m;
                            answer = [0];
                            if (discriminant >= 0) {
                                const x1 = Math.round((-k + Math.sqrt(discriminant)) / 2 * 100) / 100;
                                const x2 = Math.round((-k - Math.sqrt(discriminant)) / 2 * 100) / 100;
                                answer.push(x1, x2);
                            }
                            answer.sort((x, y) => x - y);
                        }
                        break;
                }
                
                // Удаляем дубликаты и сортируем
                answer = [...new Set(answer)].sort((a, b) => a - b);
                problems.push({ question, answer });
            }
            
            return problems;
        }
        
        // Показать текущую задачу
        function showProblem() {
            if (appState.currentProblem >= appState.problems.length) {
                showResults();
                return;
            }
            
            document.getElementById('main-menu').classList.add('hidden');
            document.getElementById('problem-section').classList.remove('hidden');
            
            const problem = appState.problems[appState.currentProblem];
            
            // Обновляем UI
            document.getElementById('block-title').textContent = 
                `${appState.blockNames[appState.currentBlock]}`;
            
            document.getElementById('problem-counter').textContent = 
                `${appState.currentProblem + 1}/${appState.problems.length}`;
            
            document.getElementById('score-counter').textContent = 
                `${appState.score}`;
            
            document.getElementById('problem-text').textContent = problem.question;
            document.getElementById('answer-input').value = '';
            document.getElementById('answer-input').focus();
            
            // Обновляем прогресс бар
            const progress = ((appState.currentProblem) / appState.problems.length) * 100;
            document.getElementById('progress-bar').style.width = `${progress}%`;
        }
        
        // Проверить ответ
        function checkAnswer() {
            const userAnswer = document.getElementById('answer-input').value.trim();
            const correctAnswer = appState.problems[appState.currentProblem].answer;
            
            if (!userAnswer) {
                showFeedback(false, 'Пожалуйста, введите ответ!', correctAnswer.join(', '));
                return;
            }
            
            try {
                // Разделяем ответы пользователя
                const userAnswers = userAnswer.split(',')
                    .map(x => x.trim())
                    .filter(x => x !== '')
                    .map(x => {
                        // Пробуем преобразовать в число
                        const num = parseFloat(x);
                        return isNaN(num) ? x : num;
                    })
                    .sort((a, b) => a - b);
                
                // Проверяем ответы
                const isCorrect = JSON.stringify(userAnswers) === JSON.stringify(correctAnswer);
                
                if (isCorrect) {
                    appState.score++;
                    showFeedback(true, 'Правильно!', correctAnswer.join(', '));
                    createConfetti();
                } else {
                    showFeedback(false, 'Неверный ответ', correctAnswer.join(', '));
                }
                
                appState.currentProblem++;
                setTimeout(showProblem, 1500);
            } catch (e) {
                showFeedback(false, 'Ошибка при проверке ответа. Проверьте формат ввода.', correctAnswer.join(', '));
                console.error(e);
            }
        }
        
        // Пропустить задачу
        function skipProblem() {
            const correctAnswer = appState.problems[appState.currentProblem].answer;
            showFeedback(false, 'Задача пропущена', correctAnswer.join(', '));
            appState.currentProblem++;
            setTimeout(showProblem, 1500);
        }
        
        // Показать обратную связь
        function showFeedback(isCorrect, message, correctAnswer) {
            const modal = document.createElement('div');
            modal.className = `fixed inset-0 flex items-center justify-center z-50 ${isCorrect ? 'bg-green-500/80' : 'bg-red-500/80'}`;
            modal.innerHTML = `
                <div class="neumorphism rounded-xl p-6 max-w-sm w-full text-center">
                    <div class="text-6xl mb-4">${isCorrect ? '✅' : '❌'}</div>
                    <h3 class="text-2xl font-bold mb-2">${message}</h3>
                    ${!isCorrect ? `<div class="bg-gray-100 dark:bg-slate-700 p-3 rounded-lg my-4">
                        <p class="text-sm">Правильный ответ:</p>
                        <p class="font-mono font-bold">${correctAnswer}</p>
                    </div>` : ''}
                    <button onclick="this.parentElement.parentElement.remove()" class="mt-4 ${isCorrect ? 'btn-primary' : 'bg-red-500 hover:bg-red-600'} text-white font-bold py-2 px-6 rounded-lg">
                        Продолжить
                    </button>
                </div>
            `;
            document.body.appendChild(modal);
        }
        
        // Создать конфетти
        function createConfetti() {
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = `${Math.random() * 100}%`;
                confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
                confetti.style.animationDuration = `${2 + Math.random() * 3}s`;
                confetti.style.animationDelay = `${Math.random() * 0.5}s`;
                document.body.appendChild(confetti);
                
                // Удаляем конфетти после анимации
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }
        
        // Показать подсказку
        function showHint() {
            document.getElementById('hint-text').textContent = appState.hints[appState.currentBlock];
            document.getElementById('hint-modal').classList.remove('hidden');
        }
        
        // Закрыть подсказку
        function closeHint() {
            document.getElementById('hint-modal').classList.add('hidden');
        }
        
        // Показать настройки
        function showSettings() {
            document.getElementById('settings-modal').classList.remove('hidden');
            document.getElementById('task-count').value = appState.settings.taskCount;
            document.getElementById('difficulty').value = appState.settings.difficulty;
        }
        
        // Закрыть настройки
        function closeSettings() {
            document.getElementById('settings-modal').classList.add('hidden');
        }
        
        // Сохранить настройки
        function saveSettings() {
            appState.settings.taskCount = document.getElementById('task-count').value;
            appState.settings.difficulty = document.getElementById('difficulty').value;
            localStorage.setItem('mathMasterSettings', JSON.stringify(appState.settings));
            closeSettings();
        }
        
        // Загрузить настройки
        function loadSettings() {
            const savedSettings = localStorage.getItem('mathMasterSettings');
            if (savedSettings) {
                appState.settings = JSON.parse(savedSettings);
            }
        }
        
        // Показать клавиатуру
        function showKeyboard() {
            document.getElementById('keyboard-modal').classList.remove('hidden');
        }
        
        // Закрыть клавиатуру
        function closeKeyboard() {
            document.getElementById('keyboard-modal').classList.add('hidden');
        }
        
        // Вставить символ
        function insertSymbol(symbol) {
            const input = document.getElementById('answer-input');
            const startPos = input.selectionStart;
            const endPos = input.selectionEnd;
            const currentValue = input.value;
            
            input.value = currentValue.substring(0, startPos) + symbol + currentValue.substring(endPos);
            input.selectionStart = input.selectionEnd = startPos + symbol.length;
            input.focus();
        }
        
        // Удалить символ
        function backspace() {
            const input = document.getElementById('answer-input');
            const startPos = input.selectionStart;
            const endPos = input.selectionEnd;
            const currentValue = input.value;
            
            if (startPos === endPos && startPos > 0) {
                input.value = currentValue.substring(0, startPos - 1) + currentValue.substring(endPos);
                input.selectionStart = input.selectionEnd = startPos - 1;
            } else {
                input.value = currentValue.substring(0, startPos) + currentValue.substring(endPos);
                input.selectionStart = input.selectionEnd = startPos;
            }
            input.focus();
        }
        
        // Показать результаты
        function showResults() {
            document.getElementById('problem-section').classList.add('hidden');
            document.getElementById('results-section').classList.remove('hidden');
            
            const totalProblems = appState.problems.length;
            const percentage = Math.round((appState.score / totalProblems) * 100);
            
            // Устанавливаем иконку результата
            const resultIcon = document.getElementById('result-icon');
            if (percentage === 100) {
                resultIcon.innerHTML = '<i class="fas fa-trophy"></i>';
                resultIcon.className = 'w-24 h-24 rounded-full bg-gradient-to-r from-yellow-400 to-yellow-600 flex items-center justify-center text-white text-4xl mx-auto mb-6 pulse';
            } else if (percentage >= 80) {
                resultIcon.innerHTML = '<i class="fas fa-star"></i>';
                resultIcon.className = 'w-24 h-24 rounded-full bg-gradient-to-r from-blue-400 to-blue-600 flex items-center justify-center text-white text-4xl mx-auto mb-6 pulse';
            } else if (percentage >= 50) {
                resultIcon.innerHTML = '<i class="fas fa-check-circle"></i>';
                resultIcon.className = 'w-24 h-24 rounded-full bg-gradient-to-r from-green-400 to-green-600 flex items-center justify-center text-white text-4xl mx-auto mb-6';
            } else {
                resultIcon.innerHTML = '<i class="fas fa-redo"></i>';
                resultIcon.className = 'w-24 h-24 rounded-full bg-gradient-to-r from-red-400 to-red-600 flex items-center justify-center text-white text-4xl mx-auto mb-6';
            }
            
            // Устанавливаем текст
            document.getElementById('result-title').textContent = 
                `Блок "${appState.blockNames[appState.currentBlock]}" завершен!`;
            document.getElementById('result-score').textContent = 
                `${appState.score} из ${totalProblems} заданий`;
            
            // Устанавливаем прогресс бар
            document.getElementById('result-progress').style.width = `${percentage}%`;
            document.getElementById('result-progress').className = 
                `h-3 rounded-full ${percentage === 100 ? 'bg-gradient-to-r from-yellow-400 to-yellow-600' : 
                 percentage >= 80 ? 'bg-gradient-to-r from-blue-400 to-blue-600' : 
                 percentage >= 50 ? 'bg-gradient-to-r from-green-400 to-green-600' : 
                 'bg-gradient-to-r from-red-400 to-red-600'}`;
            
            const resultMessage = document.getElementById('result-message');
            if (percentage === 100) {
                resultMessage.textContent = 'Идеальный результат! Вы настоящий мастер уравнений!';
                resultMessage.className = 'text-lg text-yellow-600 dark:text-yellow-400';
            } else if (percentage >= 80) {
                resultMessage.textContent = 'Отличный результат! Продолжайте в том же духе!';
                resultMessage.className = 'text-lg text-blue-600 dark:text-blue-400';
            } else if (percentage >= 50) {
                resultMessage.textContent = 'Хороший результат! Еще немного практики!';
                resultMessage.className = 'text-lg text-green-600 dark:text-green-400';
            } else {
                resultMessage.textContent = 'Попробуйте еще раз и изучите теорию внимательнее!';
                resultMessage.className = 'text-lg text-red-600 dark:text-red-400';
            }
            
            // Создаем конфетти для хороших результатов
            if (percentage >= 80) {
                createConfetti();
            }
        }
        
        // Повторить блок
        function retryBlock() {
            startBlock(appState.currentBlock);
        }
        
        // Переключить тему
        function toggleDarkMode() {
            if (localStorage.getItem('color-theme') === 'dark' || (!('color-theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.remove('dark');
                localStorage.setItem('color-theme', 'light');
                appState.settings.theme = 'light';
            } else {
                document.documentElement.classList.add('dark');
                localStorage.setItem('color-theme', 'dark');
                appState.settings.theme = 'dark';
            }
            saveSettings();
        }
        
        // Установить светлую тему
        function setLightTheme() {
            document.documentElement.classList.remove('dark');
            localStorage.setItem('color-theme', 'light');
            appState.settings.theme = 'light';
        }
        
        // Установить темную тему
        function setDarkTheme() {
            document.documentElement.classList.add('dark');
            localStorage.setItem('color-theme', 'dark');
            appState.settings.theme = 'dark';
        }
        
        // Применить тему
        function applyTheme() {
            if (appState.settings.theme === 'dark' || (appState.settings.theme === 'system' && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        }
        
        // Вспомогательная функция для генерации случайных целых чисел
        function randomInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }
    </script>
</body>
</html>
