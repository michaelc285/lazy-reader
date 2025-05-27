<script lang="ts">
  import { writable, type Writable } from 'svelte/store';
  import './app.css';

  interface AppState {
    step: number;
    text: string;
    keepPunctuation: boolean;
    speed: number;
    currentWord: string;
    currentIndex: number;
    isPlaying: boolean;
    words: string[];
  }

  const state: Writable<AppState> = writable({
    step: 1,
    text: '',
    keepPunctuation: false,
    speed: 500,
    currentWord: '',
    currentIndex: 0,
    isPlaying: false,
    words: []
  });

  function preprocessText(text: string, keepPunctuation: boolean): string[] {
    if (!keepPunctuation) {
      text = text.replace(/[.,!?;；。，！？]/g, '');
    }
    const paragraphs: string[] = text.split(/[\n。]+/).filter(p => p.trim() !== '');
    const wordArray: string[] = [];
    paragraphs.forEach((para: string, index: number) => {
      const words: string[] = para.trim().split('');
      wordArray.push(...words);
      if (index < paragraphs.length - 1) {
        wordArray.push('PAUSE');
      }
    });
    return wordArray;
  }

  function startPlayback(): void {
    state.update(s => {
      const words: string[] = preprocessText(s.text, s.keepPunctuation);
      return { ...s, step: 2, words, currentIndex: 0, isPlaying: true };
    });
  }

  function stopPlayback(): void {
    state.update(s => ({ ...s, isPlaying: false }));
  }

  function replay(): void {
    state.update(s => ({
      ...s,
      currentIndex: 0,
      currentWord: '',
      isPlaying: true
    }));
  }

  function reset(): void {
    state.set({
      step: 1,
      text: '',
      keepPunctuation: true,
      speed: 500,
      currentWord: '',
      currentIndex: 0,
      isPlaying: false,
      words: []
    });
  }

  let interval: NodeJS.Timeout | undefined;
  $: if ($state.isPlaying && $state.step === 2) {
    if (interval) clearInterval(interval);
    interval = setInterval(() => {
      state.update(s => {
        if (s.currentIndex >= s.words.length) {
          if (interval) clearInterval(interval);
          return { ...s, isPlaying: false };
        }
        const word: string = s.words[s.currentIndex];
        if (word === 'PAUSE') {
          setTimeout(() => {
            state.update(st => ({ ...st, currentIndex: st.currentIndex + 1, currentWord: '' }));
          }, 1000);
          return s;
        }
        return {
          ...s,
          currentWord: word,
          currentIndex: s.currentIndex + 1
        };
      });
    }, 60000 / $state.speed);
  } else {
    if (interval) clearInterval(interval);
  }
</script>

<div class="container">
  {#if $state.step === 1}
    <h1>懶鬼閱讀器</h1>
    <textarea
      bind:value={$state.text}
      placeholder="請輸入要閱讀的文字..."
    ></textarea>
    <div class="checkbox-container">
      <label>
        <input
          type="checkbox"
          bind:checked={$state.keepPunctuation}
        />
        保留標點符號
      </label>
    </div>
    <button
      class="start"
      on:click={startPlayback}
      disabled={!$state.text.trim()}
    >
      開始
    </button>
  {:else}
    <div class="play-section">
      <h2>正在播放</h2>
      <div class="play-word">
        {$state.currentWord || ' '}
      </div>
      <div class="slider-container">
        <label>播放速度 (字/分鐘):</label>
        <input
          type="range"
          min="100"
          max="1000"
          step="50"
          bind:value={$state.speed}
        />
        <span>當前速度: {$state.speed} 字/分鐘</span>
      </div>
      <div class="button-group">
        <button
          class="pause"
          on:click={stopPlayback}
        >
          暫停
        </button>
        <button
          class="replay"
          on:click={replay}
        >
          重播
        </button>
        <button
          class="reset"
          on:click={reset}
        >
          返回
        </button>
      </div>
    </div>
  {/if}
</div>