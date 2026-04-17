
 # Анализ обзорной статьи: Ask in Any ModalityA Comprehensive Survey on Multimodal Retrieval-Augmented Generation

**Авторы:** [ФИО авторов]  
**Журнал:** 
**Год публикации:** 
**DOI/Ссылка:** [Статья тут]

## 1. Ключевые обобщения и выводы

Есть мультимодальный запрос: вопрос q + картинка I. Обычный VLM часто не знает нужный факт из мира, а если добавить retrieval, то появляются две проблемы: трудно правильно сформулировать поиск из текста и картинки вместе, и retrieved knowledge часто шумный. Поэтому авторы строят RORA-VLM как robust multimodal RAG для knowledge-intensive VQA.

1. Первый этап retrieval: поиск по картинке.
Сначала берут query image целиком и через CLIP image encoder строят один глобальный embedding. По нему ищут похожие изображения в базе WIT. Для каждого найденного изображения достают связанный с ним entity name + background description. Это этап Image-anchored Entity Retrieval.

2. Второй этап retrieval: расширение текстового запроса и поиск текста.
Дальше исходный вопрос q расширяют найденными на первом этапе именем сущности и описанием. Уже этим расширенным запросом делают text retrieval через Google/Serper и получают несколько текстовых сниппетов. То есть двухэтапность такая: image retrieval -> query expansion -> text retrieval.

3. Сборка retrieved context.
Для каждой найденной гипотезы формируется multimodal knowledge snippet:
retrieved image + entity description + retrieved texts.
Потом несколько таких snippet’ов подаются в модель как внешний контекст.

4. Защита от шумного retrieval при обучении.
Так как retrieval ошибается, авторы на обучении специально подмешивают нерелевантный snippet. Модель учится не слепо верить retrieved context, а выбирать, какой кусок полезен, а какой шум. Это их adversarial noise injection.

5. Query-oriented visual token refinement.
Параллельно они фильтруют визуальную часть. Картинка кодируется CLIP не только в один глобальный вектор, но и в последовательность visual tokens, где каждый токен соответствует patch’у изображения. Для query image оставляют только токены, наиболее релевантные тексту вопроса; для retrieved images — токены, наиболее релевантные query image. Это не новый этап поиска, а очистка визуального контекста от фона и мусора.

6. Подача в VLM и генерация ответа.
Очищенные visual tokens и retrieved texts подаются в backbone LLaVA-v1.5 как interleaved multimodal context. Нового специального адаптера типа Q-Former авторы не вводят; они используют обычный VLM-backbone с projection layer и улучшают именно retrieval и robustness.

7. Что в итоге дает метод.
По результатам статьи, этот пайплайн дает заметный прирост на OVEN, InfoSeek и Enc-VQA, улучшает retrieval precision, помогает лучше переживать шумный retrieval и дает неплохой zero-shot transfer на unseen domains. Авторы отдельно подчеркивают, что выигрывает именно связка: двухшаговый retrieval + noise robustness + visual token refinement.

## 2. Бенчмарки, датасеты 


## 3. Полезные ссылки


## 4. Итог
использют двух этапный retirever, сначала чисто картинки по cLIP, потом реракнинг по BLIP-2










