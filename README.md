# 🤖 AI News Automation Agent (LangGraph & X Integration)

## 📌 概要
最新のニュースを自動取得し、AIが要約、そしてSNS（X/Twitter）への投稿までをワンストップで行う自律型AIエージェントです。
単なる自動化ではなく、**LangGraph** を用いた「ReAct」パターンを採用しており、ユーザーの要求に応じてエージェントが自律的に「ニュース取得」「要約」「投稿」のツールを選択・実行します。

## ✨ 主な機能
- **自律的エージェント (LangGraph)**: ユーザーの曖昧な指示を解釈し、必要なステップを判断して実行します。
- **最新ニュース取得 (NewsAPI)**: 世界中のメディアから指定キーワードに合致する最新記事を一件抽出します。
- **インテリジェント要約 (OpenAI GPT-4o-mini)**: Xの制限文字数（140字）に合わせ、重要度を維持したまま自然な日本語で要約します。
- **SNS自動連携 (Tweepy)**: X APIを利用し、生成された要約をシームレスに投稿します。
- **インタラクティブUI (Gradio)**: ブラウザ上で誰でも簡単にエージェントを操作できるユーザーインターフェースを搭載しています。

## 🛠 技術スタック
- **Framework**: `LangGraph`, `LangChain`
- **LLM**: `GPT-4o-mini`
- **API**: `NewsAPI`, `X API (v2)`
- **Library**: `Tweepy`, `Gradio`, `Requests`
- **Environment**: Google Colab

## 🚀 ワークフロー
エージェントは以下のプロセスを自律的にループし、タスクを完遂します。

1. **Plan**: ユーザーの入力（例：「AIのニュースを投稿して」）を分析
2. **Action (Search)**: `get_news` ツールで最新記事を収集
3. **Action (Summarize)**: `summarize` ツールで内容を140字以内に圧縮
4. **Action (Post)**: `post_tweet` ツールでXに投稿
5. **Report**: 実行結果（投稿内容とツイートID）をユーザーに報告



## 💡 こだわったポイント
- **LangGraphの採用**: 従来のシーケンシャルな（順序通りの）実行ではなく、エージェントが「今、何をすべきか」を判断する柔軟な設計にしました。
- **実用的なUI**: CUI（黒い画面）だけでなく、Gradioを採用することで、非エンジニアでも利用できる「プロダクト」としての完成度を意識しました。
- **プロンプトエンジニアリング**: 140字という制約の中で、ニュースの要点を逃さない要約プロンプトを構築しました。

## 📝 実行方法

本プログラムは Google Colab 環境での動作を想定しています。

1. **ファイルの準備**
   - リポジトリ内の `news-auto-agent.ipynb` をダウンロードし、ご自身の Google Colab にアップロードして開いてください。

2. **APIキーの設定**
   - Google Colab の「シークレット（鍵アイコン）」機能を使用し、以下のキーを登録してください。
     - `OPENAI_API_KEY`
     - `NEWS_API_KEY`
     - `X_API_KEY` / `X_API_KEY_SECRET`
     - `ACCESS_TOKEN` / `ACCESS_TOKEN_SECRET`
     - `BEARER_TOKEN`

3. **実行**
   - 全てのセルを順に実行してください。
   - 最後に表示される Gradio のURL（Public URL）をクリックすると、ブラウザ上でニュースの取得・要約・投稿をテストできます。
