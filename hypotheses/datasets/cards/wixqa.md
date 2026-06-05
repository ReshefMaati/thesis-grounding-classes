---
dataset_id: wixqa
dataset_name: WixQA
paper_or_description_url: https://arxiv.org/abs/2505.08643
dataset_download_url: https://huggingface.co/datasets/Wix/WixQA
corpus_download_url: https://huggingface.co/datasets/Wix/WixQA
license: MIT
domain: enterprise_customer_support
document_source_type:
  - help_center_articles
  - product_support_knowledge_base
corpus_scope: "Snapshot of the English Wix Help Center knowledge base, dated 2024-12-02, with QA configs grounded in article_ids."
corpus_availability_status: full_corpus_available
pilot_priority: 1
dataset_fetch_steps:
  - "Install/use Hugging Face datasets."
  - "load_dataset('Wix/WixQA', 'wixqa_expertwritten')"
  - "load_dataset('Wix/WixQA', 'wixqa_simulated')"
  - "load_dataset('Wix/WixQA', 'wixqa_synthetic')"
corpus_fetch_steps:
  - "load_dataset('Wix/WixQA', 'wix_kb_corpus')"
  - "Map each QA row article_ids to corpus rows by id."
data_format:
  - HuggingFace dataset configs
  - Parquet-backed dataset viewer
splits:
  - train
question_count: "200 expertwritten, 200 simulated, 6221 synthetic"
document_count: "6221 KB corpus rows"
record_fields:
  - question
  - answer
  - article_ids
answer_fields:
  - answer
evidence_fields:
  - article_ids
source_document_fields:
  - id
  - url
  - contents
  - article_type
document_content_availability: full_html_stripped_article_text
metadata_fields:
  - id
  - url
  - article_type
  - config_name
table_or_structured_data_fields: []
existing_annotations:
  - article_ids_as_ground_truth_documents
  - expert_review_for_expertwritten_answers
  - validation_for_simulated_and_synthetic_configs
unanswerable_or_ambiguous_policy: "Out-of-scope uses are documented; no explicit unanswerable split observed in card."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
normalization_risks:
  - "ExpertWritten and Simulated originate from tickets/chats, but answers are grounded in the KB corpus; keep the KB as the source-of-truth object."
  - "Synthetic split is single-doc and may overrepresent local textual evidence."
  - "Need verify whether all article_ids resolve cleanly to corpus rows."
pilot_value: "High. Best first candidate for product/support KB with full corpus and explicit article grounding."
blocking_questions:
  - "Should the pilot use expertwritten only, or combine expertwritten and simulated?"
  - "Do feature_request and known_issue article types count as source-of-truth documents or separate metadata cases?"
sources:
  - https://huggingface.co/datasets/Wix/WixQA
  - https://arxiv.org/abs/2505.08643
---

# דאטהסט: WixQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2025.

הערכה למרכזיות בהערכות RAG רחבות: נמוכה-בינונית כרגע. WixQA הוא דאטהסט חדש יחסית ולכן עדיין אינו benchmark קלאסי שחוזר ברוב עבודות RAG הרחבות. עם זאת, הוא רלוונטי מאוד למחקר שלנו משום שהוא בנוי סביב מאגר KB מוצרי סגור, עם שאלות ותשובות שמקורקעות במאמרי Help Center. לכן הוא חשוב יותר כפיילוט Enterprise/Support RAG מאשר כ-benchmark רוחבי ומבוסס היטב בקהילה.

הדאטהסט WixQA הוא מועמד חזק מאוד לפיילוט ראשון משום שהוא הכי קרוב למאגר ידע מוצרי-תמיכתי סגור: יש snapshot של Wix Help Center, יש שאלות ותשובות, ויש `article_ids` שמקשרים את השאלות למסמכי ה-KB. בניגוד לדאטסטים שבהם הקורפוס לא ברור או לא זמין, כאן נראה שיש דרך ישירה להביא גם את השאלות וגם את הקורפוס, ולשחזר אילו מאמרים שימשו כמקורות הקרקוע.

האמינות שלו טובה יחסית לשלב שלנו: הוא נוצר על ידי Wix AI Research, משוחרר ב-Hugging Face, ומלווה במאמר. היתרון המרכזי הוא שהקורפוס עצמו זמין כטקסט מלא מנורמל, עם מזהי מסמכים וכתובות URL. זה מתאים מאוד לעקרון `maximum available context`.

הסיכון העיקרי הוא שהשאלות בחלק מהקונפיגורציות מגיעות במקור מטיקטים או מצ'אטים. לפי התיחום שלנו, מקור האמת אינו הטיקט או הצ'אט, אלא מאמרי ה-Help Center שאליהם התשובות מקורקעות. לכן בפיילוט צריך להתמקד בשחזור הקרקוע דרך ה-KB ולא להתייחס לטיקטים כאל מסמכי אמת.

מבחינת מחלקות הקרקוע, WixQA צפוי להיות חזק לראיות טקסטואליות, מטאדאטה בסיסית של מסמכים, ואולי גם אונטולוגיה ארגונית סביב מוצרים, פיצ'רים, הגדרות ותהליכי שימוש. הוא כנראה פחות חזק לאגרגציה רחבה, ולכן כדאי לצמד אותו לדאטסט פיננסי או טבלאי בפיילוט.

## מבנה המידע

### הקורפוס

הקורפוס הוא snapshot של Wix Help Center באנגלית. מבחינת התזה, זה יתרון משמעותי: מדובר במאגר מסמכי ידע מוצרי שנועד להיות מקור אמת למשתמשים ולצוותי תמיכה, ולא בהתכתבות, פורום או מערכת ניהול משימות. כל מסמך בקורפוס הוא מאמר KB עם מזהה יציב, URL ציבורי, טקסט מלא לאחר ניקוי HTML, וסוג מאמר.

השדות המרכזיים בקורפוס:

- `id`: מזהה מסמך יציב. זהו השדה שאליו `article_ids` בדאטהסט מצביעים.
- `url`: כתובת מאמר התמיכה.
- `contents`: תוכן טקסטואלי מלא של המאמר, לאחר הסרת HTML.
- `article_type`: סוג המאמר, למשל `article`, `feature_request`, או `known_issue`.

איכות הקורפוס גבוהה יחסית לפיילוט ראשוני: הוא סגור, מנורמל, זמין להורדה, וכולל קישור ישיר בין שאלות למסמכי המקור. הסיכון המרכזי הוא שחלק מסוגי המאמרים, כמו feature requests או known issues, עשויים להיות פחות "מסמך אמת" קלאסי ויותר סטטוס מוצרי. לכן בפיילוט צריך לבדוק האם הם מתויגים כמטאדאטה, כראיה טקסטואלית, או כישות/מצב מוצרי.

### הדאטהסט

הדאטהסט כולל שלוש תצורות QA ועוד תצורת קורפוס:

- `wixqa_expertwritten`: שאלות משתמש אמיתיות עם תשובות מומחה, לרוב multi-document.
- `wixqa_simulated`: שאלות ותשובות שנגזרו מדיאלוגים בין משתמשים למומחים.
- `wixqa_synthetic`: שאלות סינתטיות, בדרך כלל סביב מאמר יחיד.
- `wix_kb_corpus`: מאגר מאמרי ה-KB עצמו.

השדות המרכזיים ברשומת QA:

- `question`: שאלת המשתמש.
- `answer`: תשובה בפורמט Markdown.
- `article_ids`: רשימת מזהי מאמרים שנדרשים לצורך המענה.

לצורך הפיילוט, התצורה המומלצת להתחלה היא `wixqa_expertwritten`, כי היא גם קטנה מספיק לבדיקה ידנית וגם קרובה יותר לשאלות אמיתיות. לאחר מכן אפשר להוסיף את `wixqa_simulated` כדי לבדוק האם התיוג נשאר יציב.

### דגימות מהדאטהסט

הדגימות הבאות נלקחו מתוך `wixqa_expertwritten/test.jsonl`, יחד עם מיפוי ראשוני של `article_ids` למסמכי הקורפוס.

#### דגימה 1

- שאלה (`question`): Can I start accepting payments on my site while my Wix Payments account is still under verification?
- תשובה (`answer`): You can start accepting payments on your site using Wix Payments almost immediately. However, Wix needs to verify your identity before the account can be fully activated.
- `article_ids`: `49d9e88fadbf11fa4e685c847590078ff9394c2fe7566094f504f53ca4aca465`
- מסמך מקור: `Wix Payments Verification Process`
- `article_type`: `article`
- קישור (`url`): https://support.wix.com/en/article/wix-payments-verification-process
- תקציר תוכן מקור: המאמר מסביר שאפשר להתחיל לקבל תשלומים כמעט מיד, אך נדרש תהליך אימות זהות לפני הפעלה מלאה.

#### דגימה 2

- שאלה (`question`): I am inquiring about purchasing the yearly premium plan for $17.00, which includes a free domain for 1 year. However, the voucher does not show up at checkout. Do I need to purchase the plan first and then will the voucher be available to activate?
- תשובה (`answer`): The voucher becomes available after completing the yearly Premium plan purchase. It can then be claimed from the Premium Vouchers page and is valid for two months, subject to eligibility conditions.
- `article_ids`: `06535db983ea0ffe0214af14497a1d158f279d92c92f211e87b8820aa95dbe43`
- מסמך מקור: `Using Your Free 1 Year Domain Voucher`
- `article_type`: `article`
- קישור (`url`): https://support.wix.com/en/article/using-your-free-1-year-domain-voucher
- תקציר תוכן מקור: המאמר מתאר את קבלת הווצ'ר לדומיין חינם לשנה לאחר רכישת תוכנית שנתית או רב-שנתית.

#### דגימה 3

- שאלה (`question`): I'm want to know how much it would cost to upgrade my email plan.
- תשובה (`answer`): The user should go to Email Marketing in the site dashboard, click Upgrade under Monthly Balance, choose a plan, and complete checkout.
- `article_ids`: `de6e96935f0b3321cf29416ec164482247b5035f1d2e12b36e203be8126ca8b8`
- מסמך מקור: `Email Marketing: Upgrading Your Email Marketing Plan`
- `article_type`: `article`
- קישור (`url`): https://support.wix.com/en/article/email-marketing-upgrading-your-email-marketing-plan
- תקציר תוכן מקור: המאמר מסביר כיצד לשדרג תוכנית Email Marketing מתוך הדשבורד.

#### דגימה 4

- שאלה (`question`): I want to know if the Wix store function work for selling services instead of just physical goods
- תשובה (`answer`): Wix Stores is aimed at selling products, while Wix Bookings is the relevant product for booking and paying for services.
- `article_ids`: `a513a215c1798f329293330cb5f5e975a18978954b5ee27d84441e029f900d51`, `b9ba8c318ee75f49eaa89c1d5b8d461fa2b4c27167381b869aeb31027d7187f9`
- מסמכי מקור: `Wix Stores: About Wix Stores`; `Wix Bookings: About Wix Bookings`
- `article_type`: `article`
- קישור (`url`): https://support.wix.com/en/article/wix-stores-about-wix-stores ; https://support.wix.com/en/article/wix-bookings-about-wix-bookings
- תקציר תוכן מקור: הדוגמה דורשת השוואה בין שני מוצרי Wix, ולכן היא מעניינת במיוחד למחלקת אונטולוגיה ארגונית סביב מוצרים ותפקודיהם.

#### דגימה 5

- שאלה (`question`): How can I add discounts to my service prices when customers pay for a plan?
- תשובה (`answer`): Create discount coupons for pricing plans, choose discount type, code, applicable plan, billing cycle behavior, validity dates, and usage limits.
- `article_ids`: `8cc75fbcc571336d1ef1768e7727bd9d1e6c1333f22eeb5366232b9a1a066418`
- מסמך מקור: `Pricing Plans: Creating Discount Coupons`
- `article_type`: `article`
- קישור (`url`): https://support.wix.com/en/article/pricing-plans-creating-discount-coupons
- תקציר תוכן מקור: המאמר מפרט כיצד ליצור קופונים לתוכניות תמחור, כולל סוגי הנחה, תחולת קופון ומגבלות שימוש.
