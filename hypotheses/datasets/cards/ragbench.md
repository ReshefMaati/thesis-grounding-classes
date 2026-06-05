---
dataset_id: ragbench
dataset_name: RAGBench
paper_or_description_url: https://arxiv.org/abs/2407.11005
dataset_download_url: https://huggingface.co/datasets/galileo-ai/ragbench
corpus_download_url: https://huggingface.co/datasets/galileo-ai/ragbench
license: cc-by-4.0
domain: multi_domain_rag_evaluation
document_source_type:
  - provided_rag_contexts
  - transformed_component_datasets
  - manuals
  - legal_contracts
  - financial_reports
  - research_abstracts
  - web_or_wikipedia_passages
corpus_scope: "Unified RAG-format wrapper over 12 component datasets. Hugging Face currently reports 95,381 rows; the paper describes about 100k RAG examples."
corpus_availability_status: provided_contexts_available_original_corpora_vary
pilot_priority: 2
dataset_fetch_steps:
  - "Use Hugging Face datasets."
  - "load_dataset('galileo-ai/ragbench', '<subset>') for a specific subset."
  - "Available subsets include covidqa, cuad, delucionqa, emanual, expertqa, finqa, hagrid, hotpotqa, msmarco, pubmedqa, tatqa, techqa."
  - "Each subset has train, validation, and test splits."
corpus_fetch_steps:
  - "Use the documents field as the available RAG context for each row."
  - "For source-corpus reconstruction, fetch the original component dataset separately when possible."
  - "Do not assume RAGBench preserves original document ids, metadata, full corpus, original evidence schema, or original reasoning traces."
data_format:
  - HuggingFace dataset configs
  - parquet
  - RAG tuples
splits:
  - train
  - validation
  - test
question_count: "95,381 rows on the current Hugging Face card; paper frames it as about 100k RAG examples."
document_count: "Variable per row: examples usually contain retrieved/provided context documents, not a single unified full corpus."
record_fields:
  - id
  - question
  - documents
  - response
  - generation_model_name
  - annotating_model_name
  - dataset_name
  - documents_sentences
  - response_sentences
  - sentence_support_information
  - unsupported_response_sentence_keys
  - adherence_score
  - overall_supported_explanation
  - relevance_explanation
  - all_relevant_sentence_keys
  - all_utilized_sentence_keys
  - trulens_groundedness
  - trulens_context_relevance
  - ragas_faithfulness
  - ragas_context_relevance
  - gpt3_adherence
  - gpt3_context_relevance
  - gpt35_utilization
  - relevance_score
  - utilization_score
  - completeness_score
answer_fields:
  - response
  - response_sentences
evidence_fields:
  - documents
  - documents_sentences
  - all_relevant_sentence_keys
  - all_utilized_sentence_keys
  - sentence_support_information.supporting_sentence_keys
source_document_fields:
  - documents
  - dataset_name
document_content_availability: retrieved_or_selected_contexts_only
metadata_fields:
  - id
  - dataset_name
  - generation_model_name
  - annotating_model_name
table_or_structured_data_fields:
  - table_text_in_documents_for_finqa_and_tatqa
existing_annotations:
  - adherence_score
  - relevance_score
  - utilization_score
  - completeness_score
  - sentence_level_support
  - relevant_sentence_keys
  - utilized_sentence_keys
unanswerable_or_ambiguous_policy: "Not primarily an unanswerable-QA dataset. Some component examples include unsupported or hallucinated generated responses; labels focus on support by provided contexts."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
  - aggregation
normalization_risks:
  - "RAGBench normalizes source datasets into retrieved contexts, which can erase original corpus structure."
  - "Many original answers are ignored and regenerated with LLMs, so the response is not always the original human or expert answer."
  - "Metadata, document hierarchy, original evidence ids, table schemas, reasoning programs, and retrieval traces may be missing."
  - "The labels indicate which retrieved sentences are useful or used, not what a human had to do to find the sources in the original corpus."
  - "FinQA and TAT-QA preserve text/table snippets but may lose original reasoning programs or richer table/report metadata."
pilot_value: "High as a secondary/control benchmark for testing the labeling agent on standardized RAG contexts; risky as the sole basis of the thesis."
blocking_questions:
  - "For each promising subset, what source information is lost relative to the original dataset?"
  - "Can the agent infer grounding-source classes from retrieved contexts alone, or does it need original corpus metadata and evidence schema?"
  - "Should RAGBench be used as a bridge benchmark after a pilot on original datasets rather than as the main corpus?"
sources:
  - https://arxiv.org/abs/2407.11005
  - https://arxiv.org/html/2407.11005
  - https://huggingface.co/datasets/galileo-ai/ragbench
  - https://github.com/rungalileo/ragbench
---

# דאטהסט: RAGBench

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2024. גרסת arXiv הראשונה הוגשה ביוני 2024, וגרסה מעודכנת הופיעה בינואר 2025.

הערכה למרכזיות בהערכות RAG רחבות: גבוהה עבור הערכת מערכות RAG, ובעיקר עבור מדדי faithfulness, relevance, utilization ו-completeness. RAGBench הוא benchmark רחב ומוכר יחסית שמאגד 12 תתי-דאטהסטים בפורמט אחיד, עם כ-95 אלף דוגמאות זמינות ב-Hugging Face וכ-100 אלף לפי ניסוח המאמר. מבחינת התזה שלנו, המרכזיות שלו חשובה אבל מורכבת: הוא חזק מאוד כנקודת השוואה ל-RAG evaluation, אך פחות נקי כקורפוס מקור שממנו ניתן לשחזר את תהליך מציאת מקורות הקרקוע.

הערך המרכזי של RAGBench הוא שהוא מציע פורמט RAG אחיד: שאלה, מסמכי context, תשובה שנוצרה על ידי מודל, ופירוק עשיר של אילו משפטים במסמכים רלוונטיים, אילו משפטים נוצלו בתשובה, ואילו משפטים בתשובה נתמכים במסמכים. זה הופך אותו למועמד חזק לבדיקת סוכן תיוג על דוגמאות שכבר עברו סטנדרטיזציה.

הסיכון המרכזי הוא שאותה סטנדרטיזציה היא גם איבוד מידע. RAGBench אינו תמיד שומר את הקורפוס המקורי המלא, את היררכיית המסמכים, את המטאדאטה, את תוכניות החישוב המקוריות, או את מסלול ההבאה של הראיות. לכן הוא מתאים יותר כ-benchmark משני או כ-control, ופחות כתחליף מלא לדאטהסטים המקוריים.

## מה RAGBench מספק

הדאטהסט כולל 12 תתי-דאטהסטים: `covidqa`, `cuad`, `delucionqa`, `emanual`, `expertqa`, `finqa`, `hagrid`, `hotpotqa`, `msmarco`, `pubmedqa`, `tatqa`, ו-`techqa`.

התחומים המכוסים הם מחקר ביו-רפואי, ידע כללי, חוזים משפטיים, תמיכת לקוחות, מדריכים טכניים ופיננסים. לפי המאמר, מטרת הבחירה הייתה לכסות דומיינים תעשייתיים ורלוונטיים ליישומי RAG בעולם אמיתי.

המבנה האחיד של כל רשומה הוא tuple של `question`, `documents`, ו-`response`, יחד עם תוויות TRACe. התוויות המרכזיות הן `relevance_score`, `utilization_score`, `completeness_score`, ו-`adherence_score`. בנוסף יש תוויות ברמת משפטים: `all_relevant_sentence_keys`, `all_utilized_sentence_keys`, ו-`sentence_support_information`.

המסמך המקורי של RAGBench מדגיש שהמטרה אינה רק תשובה נכונה, אלא הערכה של שני רכיבי RAG: האם ה-retriever הביא context רלוונטי, והאם ה-generator השתמש בו ונשאר נאמן אליו. זה קרוב לשאלת התזה, אבל לא זהה לה: אצלנו השאלה היא איזה סוג מקור קרקוע נדרש כדי להכין את מקורות המענה מלכתחילה.

## הקורפוס

הנקודה החשובה ביותר: ל-RAGBench אין קורפוס מקור אחד. יש לו contexts שסופקו או נשלפו מתוך תתי-דאטהסטים קיימים. לכן `documents` ברשומה הוא לא בהכרח "כל המסמך", אלא בדרך כלל קטעי context שנבחרו, הובאו או נוצרו כחלק מהמרת הדאטהסט המקורי לפורמט RAG.

בחלק מהתתי-דאטהסטים זה עדיין נראה קרוב למסמך מקור. למשל `emanual` ו-`delucionqa` מבוססים על מדריכי משתמש, ו-`cuad` מכיל חוזים ארוכים יחסית. לעומת זאת, בדאטהסטים כמו `finqa` ו-`tatqa`, המסמך מופיע בדרך כלל כטקסט וטבלה שעברו חילוץ וייצוג טקסטואלי, ולא בהכרח כמסמך פיננסי מלא עם כל המטאדאטה שלו.

ההבחנה הזו קריטית לפיילוט. אם משתמשים ב-RAGBench בלבד, אפשר לתייג "מה היה נדרש מתוך ה-context שהובא". קשה יותר לתייג "מה היה נדרש כדי להגיע ל-context הזה מתוך מאגר המסמכים המקורי".

## הדאטהסט

הדאטהסט נבנה על ידי המרה של דאטהסטים קיימים לפורמט RAG אחיד. לפי המאמר, ברוב התתי-דאטהסטים התשובות המקוריות אינן משמשות כתשובות סופיות; במקום זאת, RAGBench מייצר תשובות חדשות עם מודלים כגון GPT-3.5 ו-Claude 3 Haiku. החריגים המרכזיים הם HAGRID ו-ExpertQA, שבהם כבר היו תשובות LLM מקוריות.

התוויות נוצרו בעיקר באמצעות GPT-4 כמתייג, עם בדיקות alignment מול תתי-קבוצות אנושיות, בעיקר DelucionQA. התווית אינה "מחלקת מקור קרקוע" אלא תווית הערכה של RAG: האם המשפט בתשובה נתמך, אילו משפטים במסמכים רלוונטיים, ואילו משפטים נוצלו בפועל.

מבחינת התזה, זה נכס רציני: אפשר לבקש מסוכן התיוג לבנות "תוכנית פעולה" מתוך השאלה, המסמכים, התשובה ותוויות המשפטים. עם זאת, זו תהיה תוכנית פעולה משוחזרת על בסיס context נתון, לא שחזור מלא של פעולת אדם או מערכת מול הקורפוס המקורי.

## דגימות מהדאטהסט

דגימה מתוך `emanual`: השאלה היא "How do I select Natural mode?". הרשומה כוללת 3 מסמכי context מתוך מדריך Samsung TV. התשובה מסבירה לנווט ל-Settings, Picture, Picture Mode ולבחור Natural mode. תוויות RAGBench מסמנות שהמשפט על האפקט של Natural mode נתמך ישירות, אבל חלק מנתיב הניווט אינו נתמך במפורש. מבחינת מחלקות הקרקוע, זו דוגמה חזקה למחלקה 1, עם אפשרות למחלקה 2 אם מתייחסים לנתיב התפריטים כמבנה/מטאדאטה של המדריך.

דגימה מתוך `techqa`: השאלה היא "Why does the other instance of my multi-instance qmgr seem to hang after a failover?". הרשומה כוללת 5 מסמכי context מסוג IBM Technotes, והתשובה מייחסת את הבעיה לכשל logger בזמן restart בגלל לוגים חסרים או פגומים. מבחינת התזה, זו דוגמה מעניינת למחלקה 3 אפשרית: qmgr, failover, MSCS, logs ו-WebSphere MQ הם ישויות/רכיבים/מצבים טכניים שמתקיימים בעולם המוצרי מעבר לקטע יחיד. עם זאת, ב-RAGBench עצמו אנחנו מקבלים רק contexts ולא בהכרח את כל קורפוס ה-Technotes או המטאדאטה המוצרית.

דגימה מתוך `finqa`: השאלה היא "was initial health care trend rate higher in 2017 than 2016?". הרשומה כוללת 3 מסמכי context מתוך דוחות פיננסיים, והתשובה משווה בין 8.00% ב-2017 לבין 8.25% ב-2016. מבחינת מחלקות הקרקוע, זו דוגמה למחלקה 4: לא מספיק למצוא משפט אחד, אלא צריך להשוות ערכים מתוך מבנה פיננסי. אבל ב-RAGBench חסרה בדרך כלל תוכנית החישוב המקורית של FinQA, ולכן חשוב להשוות לגרסה המקורית של FinQA.

דגימה מתוך `tatqa`: השאלה היא "What was the decrease in the Other expense, net in 2018?". הרשומה כוללת context טבלאי וטקסטואלי, והתשובה נותנת ערך של 4.3 מיליון דולר. זו דוגמה טובה למחלקה 4, משום שהמקור כולל טבלה פיננסית והמשימה היא חילוץ/חישוב/השוואה על ערכים מובנים. מצד שני, השדות מופיעים כייצוג טקסטואלי של טבלה, ולכן צריך לבדוק האם נוח לסוכן לזהות שמדובר בטבלה ולא רק ברצף טקסט.

דגימה מתוך `cuad`: השאלה היא האם חוזה כולל דרישה להפקיד source code ב-escrow אצל צד שלישי. הרשומה כוללת חוזה ארוך אחד, והתשובה אומרת שלא נמצא סעיף כזה. מבחינת התזה, זו דוגמה שיכולה להיראות כמו מחלקה 1 כי יש חוזה כטקסט, אבל רעיונית היא קרובה למחלקה 3: השאלה נשאלת על קטגוריית סעיף משפטית, זכויות, התחייבויות ואירועי סף. כלומר היא דורשת לזהות יחס משפטי/אונטולוגי בתוך מסמך ארוך, לא רק למצוא קטע טקסט מקומי.

דגימה מתוך `delucionqa`: השאלה היא "How many batteries does the Stop/Start system need?". הרשומה מבוססת על מדריך Jeep Gladiator, והתשובה אומרת שהמערכת צריכה שתי סוללות. זו דוגמה פשוטה יחסית למחלקה 1, אולי עם נגיעה למחלקה 3 כי Stop/Start היא ישות/מערכת ברכב. היא שימושית כנקודת בקרה לשאלות שבהן RAGBench דווקא שומר context מספיק.

## התאמה למחקר שלנו

ההתאמה למחקר גבוהה אם משתמשים ב-RAGBench כמעבדת בדיקה לסוכן תיוג: הוא מאפשר לתת לסוכן שאלה, תשובה, context, משפטים רלוונטיים ומשפטים מנוצלים, ולשאול האם אפשר לשחזר תוכנית פעולה ולתרגם אותה למחלקות הקרקוע.

ההתאמה נמוכה יותר אם משתמשים בו כבסיס יחיד להוכחת התזה. הסיבה היא שהטענה שלנו עוסקת במיפוי מקורות הקרקוע הנדרשים במאגר מסמכים סגור ומטויב. RAGBench כבר עומד אחרי שלב הבאת ה-context, ולכן הוא עשוי להסתיר בדיוק את הקושי שאנחנו רוצים למדוד: האם היה צריך לנווט במסמכים, במטאדאטה, בישות ארגונית או באגרגציה על מידע מובנה כדי להגיע למקורות.

היתרון הגדול הוא שרוב מחלקות הקרקוע עשויות להופיע בו: `emanual`, `delucionqa`, `hotpotqa`, `pubmedqa` ו-`msmarco` צפויים להיות חזקים למחלקה 1; `emanual`, `techqa` ו-`delucionqa` עשויים להכיל נגיעות למחלקה 2; `techqa` ו-`cuad` עשויים לתת דוגמאות למחלקה 3; `finqa` ו-`tatqa` צפויים להיות חזקים למחלקה 4.

המסקנה האופרטיבית היא לא לפסול אותו, אלא למקם אותו נכון: RAGBench יכול להיות שכבת benchmark רחבה אחרי שנבנה תהליך תיוג על דאטהסטים מקוריים. לחלופין, אפשר להריץ פיילוט מצומצם עליו כדי לבדוק אם הסוכן מצליח לזהות מחלקות גם כאשר המידע שטוח ומנורמל. אבל התזה לא צריכה להישען עליו לבדו בלי בדיקת איבוד מידע מול הדאטהסטים המקוריים.

## שאלות פתוחות לפיילוט

שאלה ראשונה היא האם תיוג על RAGBench-only ייתן תוצאות יציבות. אם כן, זה יאפשר להשתמש בו כסט גדול ומהיר למדידה.

שאלה שנייה היא האם התיוג משתנה כאשר משווים את אותה משפחת שאלות ב-RAGBench מול הדאטהסט המקורי. זו השאלה החשובה ביותר: אם RAGBench הופך שאלות אונטולוגיות או אגרגטיביות לשאלות ראייתיות פשוטות, הוא מחליש את התזה במקום לחזק אותה.

שאלה שלישית היא האם מספיק מידע נשמר במחלקות 3-4. FinQA ו-TAT-QA כנראה נותנים הרבה מחלקה 4. לגבי מחלקה 3, הסיגנל יותר עדין: TechQA ו-CUAD נראים מבטיחים, אבל צריך לבדוק אם RAGBench שומר מספיק מטאדאטה וישויות או רק טקסט.

שאלה רביעית היא האם התוויות הקיימות של RAGBench יכולות לעזור לסוכן שלנו. לדעתי כן: `all_relevant_sentence_keys` ו-`all_utilized_sentence_keys` יכולים להיות שכבת supervision טובה לפירוק צעדים, כל עוד לא מתבלבלים בינם לבין תווית מקור הקרקוע עצמה.

