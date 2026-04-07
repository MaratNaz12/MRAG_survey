# Анализ обзорной статьи: Ask in Any ModalityA Comprehensive Survey on Multimodal Retrieval-Augmented Generation

**Авторы:** [ФИО авторов]  
**Журнал:** ACL
**Год публикации:** 2025 
**DOI/Ссылка:** [Статья тут](https://aclanthology.org/2025.findings-acl.861/)

## 1. Ключевые обобщения и выводы

Описываетс я некая эволюция раг истсем наичная с MRAG 1.0, где мультимодальность только на входе, и доп модельками все приводится к тексу. Ограничения - поетря информаци и какие-то ботлнеки в посике.
MRAG2.0 в датабазе храним оригиналные данные(модальности), а еще сам запрос может быть мультимоадльным. Также сама генеративная моделька теперь мультимодальна на вход. В поиске можем делать кросмодальный поиск, допольнительно по captions еще. 
Про MRAG3
- соханяет скрины доков
- мультимодльаный вывод у моделей 
- маршрутизация по сути добавляется для более сложных задач
гооворят про способ генерации мультимодального ответа(например можно просто выделить место в текстовом ответет и подтчавить элемнт из поиска)

выделяют 5 компонент 
Multimodal Document Parsing and Indexing (section3.1), Multimodal Search Planning
(section 3.2), Multimodal Retrieval (section 3.3), Multimodal Generation (section 3.4)

выделяют 3 типа докумнтов
неструктиваронные 
полуструктивроанные 
структированные 

обуёычно работаем.с полу и не 
работа с доками можно разделить на две типа: экстрактивные и репрезентативные
экстрактинвфй - вытаскивает из дока элементы
сначала тупо текст,  ОСР и его разватие
потом детектим еще и другие модальности (кратинки, таблицы и тд)


репрезантитвный - старатеся рбаотать с доком целостно
короче тема сейчас - дополнять все паралльеным рагом по скринам

далее про планирование рассказыается немного

далее мультимодальный поиск
retriever (section 3.3.1), reranker, and refiner

про эммбдеинги, одноканальность, многоканальност, кросмодальность, унимодальность

расказывается про генератинвый ритривал
Model Training aims to train generative models to effectively index and
retrieve documents, while enhancing the model’s capacity to memorize information from the
document corpus. This is typically achieved through sequence-to-sequence (seq2seq) training,
where the model learns to map queries to their corresponding Document Identifiers (DocIDs).

реракинг рассмтаривает как энокедр, декодер и энокедр докедоер модели,  но тут как-будто на прочь забыли что модель это просто инструмен в задаче ранжирования (point-wise, pair-wise, list-wise)
расскзаыавет про файнтюинг под скорринг?
мало про кроссмодльаный реранкер
потом говорить что можно напрмяую просить ллмки в промте скорить доки
тут кстати они вспоминают про (point-wise, pair-wise, list-wise)
но про мультимодлаьаность в этом разделе мало 

потом про refining резульатов поиска и запоса   

Про вход и выход генерации тоже пишут 

и приводят таблицу датасетов с описанием небоошьим - хорошо

## 2. Бенчмарки, датасеты 


## 3. Полезные ссылки


ссылаются на единсвтенную по их мнению актуальную обзорную статью по мультимодальным: 

Ruochen Zhao, Hailin Chen, Weishi Wang, Fangkai
Jiao, Xuan Long Do, Chengwei Qin, Bosheng Ding,
Xiaobao Guo, Minzhi Li, Xingxuan Li, and Shafiq
Joty. 2023a. Retrieving multimodal information for
augmented generation: A survey. In Findings of the
Association for Computational Linguistics: EMNLP
2023, pages 4736–4756, Singapore. Association for
Computational Linguistics.

## 4. Итог
Хорошая статья, четко подтверждает идею недостаточности структурности в вопросе проектирования MRAG. Дает полезные идеи по декомпозиции пайплана. Упомянуты вопрсоы обучения.