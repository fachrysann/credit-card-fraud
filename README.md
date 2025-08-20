🛡️ Credit Card Fraud Detection
📌 About the Dataset

Sumber: Kaggle - Credit Card Fraud Detection

Transaksi kartu kredit di Eropa, September 2013.

Periode 2 hari, total 284,807 transaksi dengan 492 kasus fraud.

Highly imbalanced → hanya 0.172% data yang fraud.

Fitur:

V1 … V28 → hasil transformasi PCA.

Time → detik sejak transaksi pertama.

Amount → jumlah transaksi.

Class → label target (1 = fraud, 0 = normal).

⚠️ Karena imbalance, metrik AUPRC (Area Under Precision-Recall Curve) lebih bermakna dibanding akurasi biasa.

📐 Formula AUPRC
AUPRC
=
∫
0
1
𝑃
𝑟
𝑒
𝑐
𝑖
𝑠
𝑖
𝑜
𝑛
(
𝑅
𝑒
𝑐
𝑎
𝑙
𝑙
)
 
𝑑
𝑅
𝑒
𝑐
𝑎
𝑙
𝑙
AUPRC=∫
0
1
	​

Precision(Recall)dRecall

atau secara diskret (approx):

AUPRC
=
∑
𝑖
=
1
𝑛
−
1
(
𝑅
𝑒
𝑐
𝑎
𝑙
𝑙
𝑖
+
1
−
𝑅
𝑒
𝑐
𝑎
𝑙
𝑙
𝑖
)
⋅
𝑃
𝑟
𝑒
𝑐
𝑖
𝑠
𝑖
𝑜
𝑛
𝑖
+
1
AUPRC=
i=1
∑
n−1
	​

(Recall
i+1
	​

−Recall
i
	​

)⋅Precision
i+1
	​

🚀 Modeling Approach

Saya menggunakan ensemble gradient boosting models yang populer untuk imbalance classification:

XGBoost → tree-based boosting, menggunakan parameter scale_pos_weight untuk imbalance.

CatBoost → boosting dengan class_weights, lebih robust dan easy-to-tune.

📊 Performance (Test Data)
Model	AUPRC	Catatan
XGBoost	0.894	Terbaik, recall tinggi, balance precision.
CatBoost	0.888	Hampir setara, lebih stabil.
🧪 Full Dataset Prediction (XGBoost GAN-trained model)

Evaluasi prediksi di seluruh dataset asli:

Total samples : 283,718

Correct preds : 283,698

Incorrect preds : 20

Accuracy : 0.9999

📌 Confusion Matrix Breakdown

True Negatives (TN): 283,239 → transaksi normal terdeteksi benar.

False Positives (FP): 6 → transaksi normal salah ditandai fraud.

False Negatives (FN): 14 → fraud lolos (kerugian potensial).

True Positives (TP): 459 → fraud berhasil ditangkap.

🏆 Insight & Business Impact

Dengan AUPRC hampir 0.90, model mampu menangkap mayoritas fraud meski dataset sangat imbalance.

Dari 492 fraud asli, model berhasil mendeteksi 459 kasus → recall ~93%.

False positives hanya 6 kasus → artinya hanya sedikit customer terganggu.

False negatives 14 kasus → ini adalah fokus perbaikan, karena setiap fraud yang lolos = potensi kerugian finansial.

🎯 Kesimpulan

XGBoost outperform CatBoost tipis pada AUPRC (0.894 vs 0.888).

Akurasi tinggi tidak berarti di kasus imbalance, tapi breakdown confusion matrix menunjukkan model sangat efektif.

Bisa dipakai sebagai fraud detection engine real-time untuk memblokir transaksi mencurigakan.
