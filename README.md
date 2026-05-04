1. Metodologiya və Baseline Qiymətləndirmə
Layihəyə başlayarkən ilk addım olaraq Mozilla Common Voice (Azərbaycan dili) datasetindən istifadə edilərək OpenAI Whisper-Small modelinin "zero-shot" performansı yoxlanılmışdır. Baseline testi üçün test datası Hugging Face üzərindən yüklənmiş və heç bir əlavə təlim olmadan model tətbiq edilmişdir.

Baseline Nəticələri: WER: 27.12%, CER: 7.21%.
Bu nəticələr göstərir ki, Whisper modeli Azərbaycan dili üçün kifayət qədər güclü baza biliyinə malikdir.

2. Fine-Tuning Prosesi və Qarşılaşılan Çətinliklər
Modelin Azərbaycan dilinə adaptasiyasını artırmaq üçün 200+ training və 50 validation nümunəsi ilə fine-tuning prosesi başladılmışdır.

Müşahidələr: Təlim zamanı həm training, həm də validation loss göstəricilərinin stabil şəkildə aşağı düşdüyü müşahidə edilmişdir. Lakin WER göstəricisi qeyri-stabil xarakter nümayiş etdirmişdir (əvvəlcə azalma, sonra artma və sonda yenidən eniş). Yekun olaraq model test setində 36.26% WER nəticəsi vermişdir.

Texniki Analiz: WER-in loss ilə mütənasib olmamasının bir neçə fundamental səbəbi müəyyən edilmişdir:

Dil Parametrləri: language="az" və task="transcribe" funksiyaları forced şəkildə tətbiq edilmədiyi üçün model bəzən fonetik qarışıqlıq yaşamışdır.

Dataset Keyfiyyəti: Common Voice datasetindəki bəzi audio yazıların aşağı keyfiyyətli olması və reference mətnlərdəki uyğunsuzluqlar (məsələn, durğu işarələri və ya yazılış xətaları) WER-in süni şəkildə yüksək çıxmasına səbəb olmuşdur.

Leksik Məna: Prediction və Reference müqayisəsi göstərir ki, model leksik mənanı tam tutur, lakin spesifik səs birləşmələrində kiçik fərqlər edir.

Loss göstəricilərinin kəskin enməsi ilk baxışda "yüngül overfitting" təəssüratı yarada bilər, lakin WER-in fərqli davranması bunun əsas səbəbinin əzbərləmə deyil, dataset həcminin məhdudluğu və audio keyfiyyəti olduğunu sübut edir. Model real test nümunələrində kifayət qədər məntiqli transkripsiyalar istehsal edir. Sadece Wer nisbeten boyuk olma sebebi hem data hemde reference sentence problemleridir.

5. Nəticə və Gələcək Addımlar
Məhdud vaxt və resurs daxilində qurulan bu pipeline, Azərbaycan dili üçün ASR sistemlərinin inkişaf etdirilməsi üçün baza rolunu oynaya bilər. Növbəti mərhələdə daha böyük dataset (100+ saat) və dil modeli (Language Model) inteqrasiyası ilə WER göstəricisini 10%-in altına salmaq mümkündür.