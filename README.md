<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fibonacci — README</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            line-height: 1.6;
            color: #24292e;
            max-width: 860px;
            margin: 0 auto;
            padding: 2rem 1.5rem;
            background: #ffffff;
        }
        h1 {
            font-size: 2rem;
            border-bottom: 1px solid #e1e4e8;
            padding-bottom: 0.3em;
            margin-bottom: 0.5em;
        }
        h2 {
            font-size: 1.5rem;
            border-bottom: 1px solid #e1e4e8;
            padding-bottom: 0.3em;
            margin-top: 1.8em;
        }
        h3 {
            font-size: 1.2rem;
            margin-top: 1.5em;
        }
        ul {
            padding-left: 1.5em;
        }
        li {
            margin: 0.3em 0;
        }
        code {
            background: #f6f8fa;
            padding: 0.2em 0.4em;
            border-radius: 4px;
            font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
            font-size: 0.9em;
        }
        pre {
            background: #f6f8fa;
            padding: 1em;
            border-radius: 6px;
            overflow-x: auto;
            font-size: 0.9em;
        }
        pre code {
            background: none;
            padding: 0;
        }
        .note {
            background: #fff5b1;
            border-left: 4px solid #ffd33d;
            padding: 0.8em 1em;
            border-radius: 4px;
            margin: 1.2em 0;
        }
        .folder {
            color: #0366d6;
            font-weight: 600;
        }
        hr {
            border: 0;
            border-top: 1px solid #e1e4e8;
            margin: 2em 0;
        }
        table {
            border-collapse: collapse;
            width: 100%;
            margin: 1em 0;
        }
        th, td {
            border: 1px solid #dfe2e5;
            padding: 0.5em 0.8em;
            text-align: left;
        }
        th {
            background: #f6f8fa;
            font-weight: 600;
        }
    </style>
</head>
<body>

<h1>Fibonacci</h1>

<p>Учебный проект по реализации вычисления чисел Фибоначчи на языке Python. Включает рекурсивный алгоритм и графический интерфейс (Tkinter) для ввода числа и замера времени выполнения.</p>

<h2>📁 Структура проекта</h2>

<table>
    <thead>
        <tr>
            <th>Путь</th>
            <th>Тип</th>
            <th>Назначение</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span class="folder">.idea/</span></td>
            <td>Папка</td>
            <td>Настройки IDE (PyCharm / IntelliJ IDEA)</td>
        </tr>
        <tr>
            <td><span class="folder">Фибоначчи/</span></td>
            <td>Папка</td>
            <td>Исходный код проекта</td>
        </tr>
        <tr>
            <td><code>Фибоначчи/fibonacci.py</code></td>
            <td>Файл</td>
            <td>Рекурсивная функция вычисления чисел Фибоначчи и тестовый запуск</td>
        </tr>
        <tr>
            <td><code>Фибоначчи/ДЗ Интерфейс для fibonacci.py</code></td>
            <td>Файл</td>
            <td>Графический интерфейс на Tkinter для ввода числа и замера времени</td>
        </tr>
    </tbody>
</table>

<h2>🔧 Реализация</h2>

<h3>fibonacci.py</h3>

<p>Содержит рекурсивную функцию <code>fibonacci(n)</code>, которая возвращает <em>n</em>-е число Фибоначчи. В конце файла выполняется тестовый вызов для <code>n = 35</code> с замером времени выполнения[reference:0].</p>

<pre><code>import time
import random
from numba import njit

def fibonacci(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

start = time.time()
data = fibonacci(35)
print(data)
print(time.time() - start)
</code></pre>

<div class="note">
    <strong>Примечание:</strong> В коде импортируется <code>numba.njit</code>, однако декоратор <code>@njit</code> не применён к функции. Это может быть заготовкой для будущей оптимизации.
</div>

<h3>ДЗ Интерфейс для fibonacci.py</h3>

<p>Скрипт создаёт графическое окно с помощью <code>tkinter</code>. Пользователь вводит число, нажимает кнопку «Запустить» — вызывается функция <code>fibonacci.fibonacci(input_number)</code>, результат и время выполнения отображаются в текстовом поле[reference:1].</p>

<pre><code>import tkinter as tk
import time
import fibonacci

class AlgorithmComparisionApp:
    def __init__(self):
        self.root = tk.Tk()
        self.root.geometry("500x700")
        self.root.title("Ряд Фибоначчи")
        self.create_widgets()

    def create_widgets(self):
        font = ("Arial", 12)
        center_frame = tk.Frame(self.root)
        center_frame.pack(expand=True)

        self.entry_label = tk.Label(center_frame, text="Введите число:", font=font)
        self.entry_label.pack()

        self.entry = tk.Entry(center_frame, font=font)
        self.entry.pack()

        self.run_button = tk.Button(center_frame, text="Запустить",
                                     command=self.run_algorithm, font=font)
        self.run_button.pack()

        self.result_text = tk.Text(center_frame, wrap=tk.WORD, font=font,
                                    height=10, width=40)
        self.result_text.pack()

        self.time_label = tk.Label(center_frame, text="Время выполнения:", font=font)
        self.time_label.pack()

    def run_algorithm(self):
        input_number = int(self.entry.get())
        start_time = time.time()
        result = fibonacci.fibonacci(input_number)
        end_time = time.time()

        self.result_text.delete("1.0", tk.END)
        self.result_text.insert(tk.END, f"Результат: {result}\n")
        self.time_label.config(
            text=f"Время выполнения: {end_time - start_time:.6f} секунд"
        )

if __name__ == "__main__":
    app = AlgorithmComparisionApp()
    app.root.mainloop()
</code></pre>

<h2>🚀 Установка и запуск</h2>

<p>Требуется Python 3.8 или выше.</p>

<pre><code># Клонирование репозитория
git clone https://github.com/Shadow2011228/fibonacci.git

# Переход в директорию проекта
cd fibonacci/Фибоначчи

# Запуск графического интерфейса
python "ДЗ Интерфейс для fibonacci.py"
</code></pre>

<p>Для запуска только алгоритма без интерфейса:</p>

<pre><code>python fibonacci.py
</code></pre>

<h2>📖 Пример использования</h2>

<p>После запуска интерфейса введите число (например, <code>10</code>) и нажмите «Запустить». В окне отобразится результат — <code>55</code> — и время выполнения. Рекурсивный алгоритм имеет экспоненциальную сложность, поэтому для больших чисел (например, <code>35</code> и выше) время выполнения может быть значительным.</p>

<h2>🎯 Цели проекта</h2>
<ul>
    <li>Реализация классического рекурсивного алгоритма вычисления чисел Фибоначчи</li>
    <li>Изучение библиотеки <code>tkinter</code> для создания графического интерфейса</li>
    <li>Измерение и визуализация времени выполнения алгоритма</li>
    <li>Выполнение учебного домашнего задания</li>
</ul>

<h2>📄 Лицензия</h2>
<p>Лицензия не указана в репозитории. По умолчанию все права принадлежат автору.</p>

<hr>
<p><em>README сгенерирован на основе анализа исходного кода репозитория. Для точного описания рекомендуется добавить собственный README.md в корень проекта.</em></p>

</body>
</html>
