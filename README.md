# SpectraLens 🎙

**Browser-native audio spectrum analyzer with MFCC / Mel spectrogram support**
**ブラウザ完結の音声スペクトル解析ツール — MFCC・メルスペクトログラム対応**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![No server required](https://img.shields.io/badge/server-not%20required-brightgreen)]()
[![Pure JavaScript](https://img.shields.io/badge/built%20with-vanilla%20JS-yellow)]()

---

## Demo / デモ

🔗 **[Live Demo](https://KAT805.github.io/spectralens/)**

> Drop any WAV / MP3 / OGG file, or click **"Run demo with synthetic signal"** to try instantly — no sign-up, no server, no data leaves your browser.
>
> WAV / MP3 / OGG ファイルをドロップするか、**「Run demo with synthetic signal」**をクリックするだけで即試せます。サインアップ不要・サーバー不要・音声データは外部送信されません。

---

## Features / 機能

### Classic Tab
| Feature | Details |
|---|---|
| Waveform | Min-max envelope rendering with gradient color |
| FFT Spectrum | 4096-point FFT with Hanning window |
| Spectrogram | Short-time Fourier transform, 8 frequency bands |
| Frequency Bands | Sub / Bass / Low-mid / Mid / Hi-mid / Presence / Brilliance |

### Mel / MFCC Tab
| Feature | Details |
|---|---|
| Mel Spectrogram | 40 mel filterbanks, log-compressed power |
| MFCC Heatmap | 13 coefficients × time, diverging colormap |
| MFCC Mean Bar Chart | Average coefficient values over entire signal |

### Δ Delta MFCC Tab
| Feature | Details |
|---|---|
| Δ Delta MFCC | 1st-order difference (velocity of spectral features) |
| ΔΔ Delta-Delta MFCC | 2nd-order difference (acceleration) |
| Delta Line Chart | C1–C6 coefficient trajectories over time |

### Stats / 統計値
`Peak Frequency` · `RMS Level (dB)` · `Sample Rate` · `Duration` · `Spectral Centroid`

---

## Privacy / プライバシー

**All processing happens inside your browser. No audio data is ever uploaded to any server.**

すべての処理はブラウザ内で完結します。音声データは一切外部サーバーに送信されません。

- ✅ No backend / サーバー不要
- ✅ No account / アカウント不要
- ✅ Works offline after first load (except Google Fonts) / 初回ロード後はオフライン動作可
- ✅ One external dependency: [Chart.js](https://www.chartjs.org/) via cdnjs CDN

---

## Usage / 使い方

### Option 1: Use the live demo / ライブデモを使う

👉 [https://KTA805.github.io/spectralens/](https://KTA805.github.io/spectralens/)

### Option 2: Run locally / ローカルで実行

```bash
git clone https://github.com/KTA805/spectralens.git
cd spectralens
# Just open index.html in your browser — no build step needed
open index.html
```

ビルド不要です。`index.html` をブラウザで開くだけで動作します。

---

## Supported Formats / 対応フォーマット

| Format | Support |
|---|---|
| WAV | ✅ Full support |
| MP3 | ✅ Full support |
| OGG | ✅ Full support |
| FLAC | ⚠️ Browser-dependent |
| AAC / M4A | ⚠️ Browser-dependent |

---

## Technical Details / 技術仕様

### Signal Processing Pipeline / 信号処理パイプライン

```
Audio File
    │
    ▼
Web Audio API (decode)
    │
    ├─── Waveform (min-max envelope)
    │
    ├─── FFT (4096-pt, Hanning window)
    │        └─── Power spectrum → Frequency bands
    │
    └─── STFT (512-pt frames, 256-pt hop)
             ├─── Mel filterbank (40 bins, 80Hz–Nyquist)
             │        └─── Log compression → Mel spectrogram
             │                 └─── DCT-II → MFCC (13 coeffs)
             │                          └─── Finite difference → Δ, ΔΔ MFCC
             └─── Magnitude → Spectrogram (8 bands)
```

### Key Parameters / 主要パラメータ

| Parameter | Value |
|---|---|
| FFT size (spectrum) | 4096 samples |
| Frame size (MFCC) | 512 samples |
| Hop size (MFCC) | 256 samples |
| Mel filterbanks | 40 bins |
| Mel frequency range | 80 Hz – Nyquist |
| MFCC coefficients | 13 |
| Delta window (N) | 2 frames |
| Display frames | up to 100 |

### Dependencies / 依存ライブラリ

| Library | Version | Purpose |
|---|---|---|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Line / bar charts |
| Web Audio API | Browser built-in | Audio decoding |
| Canvas API | Browser built-in | Heatmap rendering |

No npm, no build tools, no framework. Pure HTML + CSS + JavaScript.

npm・ビルドツール・フレームワーク不要。純粋な HTML + CSS + JavaScript で動作します。

---

## Roadmap / 今後の予定

- [ ] SNR estimation / SNR（信号対雑音比）推定
- [ ] Noise floor detection / ノイズフロア自動検出
- [ ] Export analysis report as PDF / 分析レポートのPDF出力
- [ ] Batch processing multiple files / 複数ファイルのバッチ処理
- [ ] Pitch (F0) estimation / ピッチ（基本周波数）推定
- [ ] Zero-crossing rate / ゼロ交差率
- [ ] Python backend option (FastAPI + librosa) / Pythonバックエンド対応

---

## Contributing / コントリビュート

Issues and PRs are welcome.
Issue・PRはお気軽にどうぞ。

```bash
git clone https://github.com/KTA805/spectralens.git
# Edit index.html directly — no build step
# index.html を直接編集してください。ビルド不要です。
```

---

## License / ライセンス

[MIT License](LICENSE)

---

## Author / 著者

**Kojurin**
[Zenn](https://zenn.dev/kta805) · [GitHub](https://github.com/KTA805)

> DSP / embedded engineer. Writing about audio signal processing and Python on Zenn.
> DSP・組み込みエンジニア。音声信号処理とPythonについてZennで発信しています。
