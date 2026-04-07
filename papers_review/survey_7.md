# Анализ обзорной статьи: Ask in Any ModalityA Comprehensive Survey on Multimodal Retrieval-Augmented Generation

**Авторы:** [ФИО авторов]  
**Журнал:** 
**Год публикации:** 
**DOI/Ссылка:** [Статья тут]

## 1. Ключевые обобщения и выводы


                ┌──────────────┐
                │ Text RAG     │
query ────────► │ retrieve     │ ──► reasoning ──┐
                │ + LLM        │                 │
                └──────────────┘                 │
                                                 ├──► Fusion → final answer
                ┌──────────────┐                 │
                │ Visual RAG   │                 │
query ────────► │ retrieve     │ ──► reasoning ──┘
                │ + VLM        │
                └──────────────┘


1. Retrieval (НЕ LLM)
2. Evidence Curation  ← LLM #1
3. Reasoning (CoT)    ← LLM #2
4. (для двух модальностей отдельно)
5. Fusion             ← LLM #3

Статья посвящена задаче вопросно-ответных систем по множеству документов с мультимодальным содержимым (текст, таблицы, графики, слайды). Авторы показывают, что стандартные RAG-подходы плохо работают в таких условиях: текстовые модели игнорируют важную визуальную информацию, а мультимодальные модели часто уступают в логическом рассуждении и подвержены ошибкам восприятия. Дополнительно задача усложняется тем, что информация распределена по большому числу документов, и нужно найти релевантные фрагменты среди шума — фактически «иголку в стоге сена» .
В качестве первого вклада авторы предлагают VisDoMBench — новый benchmark для multi-document multimodal QA. В отличие от существующих датасетов, он объединяет разные типы данных (текст, таблицы, графики, презентации) и требует комплексного использования нескольких документов. Также в него добавлены «отвлекающие» документы, чтобы приблизить задачу к реальным условиям и проверить способность моделей не только извлекать информацию, но и правильно локализовать источник ответа.

Основной технический вклад — архитектура VisDoMRAG, представляющая собой расширение классического RAG. Вместо одного пайплайна авторы используют два параллельных RAG-процесса: текстовый и визуальный. В каждом из них сначала выполняется retrieval (без LLM), затем LLM делает evidence curation — отбор и структурирование релевантных фрагментов, после чего строится цепочка рассуждений (chain-of-thought) и формируется ответ. Таким образом, модель не работает напрямую с «сырым» контекстом, а сначала очищает и интерпретирует его, что снижает шум и повышает точность.

Ключевая новизна заключается в этапе modality fusion: результаты двух пайплайнов (включая их reasoning) объединяются с помощью LLM, который проверяет согласованность рассуждений и синтезирует итоговый ответ. Это переносит объединение модальностей с уровня данных на уровень логики. Эксперименты показывают, что такой подход стабильно превосходит как текстовый, так и визуальный RAG, а также long-context модели, давая прирост качества порядка 12–20% .

## 2. Бенчмарки, датасеты 


## 3. Полезные ссылки
Wenhu Chen, Hexiang Hu, Xi Chen, Pat Verga, and
William W Cohen. 2022. Murag: Multimodal
retrieval-augmented generator for open question
answering over images and text. arXiv preprint
arXiv:2210.02928

мллм на таблицах 
Naihao Deng, Zhenjie Sun, Ruiqi He, Aman Sikka, Yu-
long Chen, Lin Ma, Yue Zhang, and Rada Mihalcea.
2024. Tables as images? exploring the strengths and
limitations of llms on multimodal representations of
tabular data. arXiv preprint arXiv:2402.12424.

про визуальные галюны https://arxiv.org/abs/2405.15683

In visual
question answering (VQA), (Lin and Byrne, 2022)
addresses open-domain challenges by using object
detection, image captioning, and optical character
recognition (OCR) to transform target images into
textual data.

Moving beyond text-only contexts,
MuRAG retrieves both text and image data, incor-
porating images as visual tokens (Chen et al., 2022).
RAMM enhances performance by retrieving and
encoding similar biomedical images and their cap-
tions through distinct networks (Yuan et al., 2023).

## 4. Итог


Ну типо поять вписывается в общую схему предлаагемую, делаем два независымх retrieve
далее этап фильтрации, ранжирования и траснформации происходит через vlm, 
два single-modality поиска, далее внутри каждого фильтрация и трансофрамцуия к ТЕКСТУ, (пропустили фьюз)
далее генерация (а что такое вообще фьюз модальностей, как их по сути объеденить в один спсиок? здесь просто трансформирубт все в текст и подают в модель,)

