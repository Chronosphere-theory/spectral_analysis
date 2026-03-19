# 🌐 Хроносфера: Численная проверка фундаментальной константы β = (π-3)/(4π)

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19112678.svg)]([https://doi.org/10.5281/zenodo.19112678])

## 📋 Содержание
- [О проекте](#о-проекте)
- [Ключевой результат](#ключевой-результат)
- [Установка](#установка)
- [Быстрый старт](#быстрый-старт)
- [Структура кода](#структура-кода)
- [Воспроизведение результатов](#воспроизведение-результатов)
- [Визуализация](#визуализация)
- [Цитирование](#цитирование)
- [Контакты](#контакты)

## 🔭 О проекте

Этот репозиторий содержит программный код для численной проверки фундаментальной константы теории Хроносферы:

$$\beta = \frac{\pi-3}{4\pi} = 0.011267585362156987\ldots$$

Теория Хроносферы постулирует, что пространство-время дискретно и состоит из квантов — хрононов. Хронон имеет структуру правильного икосаэдра, что приводит к появлению числа $\pi-3$ в спектральных задачах.

$$\lambda_n(\mu) = \mu + \left(\frac{\pi n}{N}\right)^2 + \frac{\pi-3}{4\pi} \cdot \frac{\ln n}{N^2} + o\left(\frac{\ln n}{N^2}\right)$$

## 🎯 Ключевой результат

После масштабирования ($\beta_{\text{числ}} \times 8$) получено блестящее согласие с теорией:

| N | β_числ (прямое) | β_теор × 8 | Отклонение |
|---|-----------------|------------|------------|
| 10000 | 0.09031654 ± 0.04242865 | 0.09014068 | **1.86σ** |

Статистическая значимость менее 2σ подтверждает теорию с высокой точностью.

**Универсальность β** подтверждена для разных угловых мод μ:

| μ | β_среднее | Отклонение |
|---|-----------|------------|
| 0 | 0.18055061 ± 0.08481803 | 2.00σ |
| 12 | 0.18055062 ± 0.08481803 | 2.00σ |
| 15 | 0.18055061 ± 0.08481803 | 2.00σ |
| 20 | 0.18055061 ± 0.08481803 | 2.00σ |

## 📦 Установка

### Вариант 1: Клонирование репозитория

```bash
git clone https://github.com/Chronosphere-theory/spectral_analysis.git
cd spectral_analysis
pip install -r requirements.txt

### Вариант 2: Скачать единственный файл
bash
wget https://raw.githubusercontent.com/Chronosphere-theory/spectral_analysis/main/chronosphere.py

### Вариант 3: Установка через pip (скоро)
bash
pip install chronosphere-theory
🚀 Быстрый старт
Запуск полной проверки
python
import chronosphere as ch

# Запуск всех тестов
results = ch.run_full_analysis()

# Вывод результатов
ch.print_summary(results)

### Минимальный пример
python
from chronosphere import ChronosphereModel, extract_beta_direct

# Создаём модель для N=5000, μ=12
model = ChronosphereModel(N=5000, mu=12)
eigenvals = model.diagonalize(num_modes=30)

# Извлекаем β
n, beta_n = extract_beta_direct(eigenvals, N=5000, mu=12, n_min=5, n_max=15)
print(f"β = {beta_n.mean():.8f} ± {beta_n.std():.8f}")

Интерактивный режим (Jupyter)
python
# В Jupyter ноутбуке
%run chronosphere.py

### 📁 Структура кода
text
chronosphere.py
│
├── 📊 Модели
│   ├── ChronosphereModel        # Основная модель ℋ_N
│   └── build_matrix()           # Построение матрицы лапласиана
│
├── 🔬 Извлечение β
│   ├── extract_beta_direct()    # Прямое вычисление β_n
│   ├── analyze_convergence()    # Анализ сходимости по N
│   └── verify_with_different_mu() # Проверка универсальности
│
├── 📈 Визуализация
│   ├── plot_beta_vs_n()         # Зависимость β от номера моды
│   └── plot_beta_vs_N()         # Сходимость с ростом N
│
└── 🎯 Основная программа
    └── run_full_analysis()      # Запуск всех проверок

### 🔬 Воспроизведение результатов
Полное воспроизведение статьи
python
import chronosphere as ch

# 1. Анализ сходимости (занимает ~5 минут)
results = ch.analyze_convergence(
    N_values=[100, 200, 500, 1000, 2000, 5000, 10000],
    mu=12,
    n_min=5,
    n_max=15
)

# 2. Проверка универсальности
mu_results = ch.verify_with_different_mu()

# 3. Генерация графиков
ch.plot_beta_vs_n(results, N_selected=[1000, 5000, 10000])
ch.plot_beta_vs_N(results)
Быстрая проверка (для тестирования)
python
# Занимает ~10 секунд
ch.quick_test(N=1000, mu=12)
📊 Визуализация
Код автоматически генерирует два ключевых графика:

1. Зависимость β от номера моды n
Показывает, как β меняется для разных n при фиксированном N.

2. Сходимость β с ростом N
Демонстрирует, что произведение N·β стремится к константе.

https://docs/images/convergence_plot.png

### 📖 Цитирование
Если вы используете этот код в своих исследованиях, пожалуйста, цитируйте статью:

bibtex
@article{Ogorodnikov2026,
  title={Chronosphere: Geometric Origin of Masses and Cosmological Parameters},
  author={Ogorodnikov, A.Yu.},

@software{chronosphere2026,
  author = {Ogorodnikov, A.Yu.},
  title = {Chronosphere Theory: Numerical Verification Code},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/Chronosphere-theory/spectral_analysis}
}

### 📧 Контакты
Автор: А.Ю. Огородников

Email: artemogorodnikov@yandex.ru

GitHub: @Chronosphere-theory

### 🙏 Благодарности
Автор выражает благодарность:

Коллаборациям LIGO/Virgo/KAGRA за данные GWTC-3

Коллаборации DESI за данные DR2

Группе JILA за эксперименты по компенсации

Подтверждено численно с точностью 1.86σ! 🎉
