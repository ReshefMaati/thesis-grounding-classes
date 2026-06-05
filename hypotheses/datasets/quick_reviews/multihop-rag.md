---
dataset_id: multihop-rag
dataset_name: MultiHop-RAG
review_status: quick_review
pilot_decision: defer
final_thesis_decision: possible_boundary_or_control
primary_reason: "חזק ל-multi-hop ולמטאדאטה, אבל מבוסס news/open-domain ולא מאגר אמת ארגוני."
relevance_summary: "מועמד טוב לשלב מאוחר או control, לא ראשון."
domain: news_open_domain
source_type:
  - news_articles
  - multi_document_evidence
  - metadata
corpus_availability_status: repository_dataset_available
next_action: "לשקול אחרי הפיילוט אם צריך בדיקת multi-hop נקייה עם metadata."
sources:
  - https://arxiv.org/abs/2401.15391
  - https://github.com/yixuantt/MultiHop-RAG
---

# MultiHop-RAG

## שורה תחתונה

MultiHop-RAG כן רלוונטי ברמה המחקרית: הוא כולל שאלות multi-hop, ראיות שמפוזרות על פני 2-4 מסמכים, וגם שימוש במטאדאטה. הוא לא פסול. הוא פשוט פחות מתאים להיות אחד הדאטהסטים הראשונים בפיילוט בגלל הדומיין והתיחום.

הדאטהסט מבוסס על מאגר מאמרי חדשות באנגלית. זה טוב לבדיקת retrieval/reasoning across documents, אבל פחות דומה למאגר מסמכי אמת ארגוני כמו KB מוצרי, technotes, חוזים, או דוחות פיננסיים. לכן בשער הראשון העדפנו דאטהסטים שמקרבים אותנו ל-source-of-truth סגור ומבוקר.

## למה לא לפיילוט ראשון

1. הדומיין הוא news/open-domain, לא מאגר ידע ארגוני או מסמכי אמת מקצועיים.
2. הערך המרכזי שלו הוא multi-hop retrieval, בעוד הפיילוט הראשון צריך לבדוק גם אונטולוגיה ארגונית ואגרגציה.
3. הוא עשוי להיות טוב מאוד ל-`textual_evidence` ול-`metadata`, אבל פחות ברור כמה הוא יאתגר את מחלקת האונטולוגיה הארגונית.
4. יש לנו כבר מועמדים חזקים יותר לפתיחה: WixQA ו-TechQA לקרבה ארגונית, MultiHiertt/FinQA/FinanceBench לאגרגציה.

## למה הוא עדיין יכול להיות שימושי

אם אחרי הפיילוט נרצה להראות שהטקסונומיה יציבה גם מול multi-hop קלאסי, MultiHop-RAG הוא מועמד טוב. הוא יכול לשמש control שמפריד בין "צריך כמה מסמכים" לבין "צריך אונטולוגיה או אגרגציה". זו הבחנה חשובה למחקר.

## למה אולי לא מצאת אותו בקבצים

קודם כול, השם המדויק הוא `MultiHop-RAG`; אם חיפשת `MultioHop-RAG`, החיפוש לא ימצא אותו. מעבר לזה, הוא לא נכלל בכרטיסים המלאים כי הסקירה הנוכחית ניסתה לבחור דאטהסטים ראשונים עם קורפוס מקור קרוב יותר ל-organization/source-of-truth.
