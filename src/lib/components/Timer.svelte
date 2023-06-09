<script lang="ts">
    import { onMount, onDestroy } from 'svelte';
    let audio: HTMLAudioElement;
    
    let time = 0;
    let timerInterval: number;
    let isRunning = false;
    let setTime = 25 * 60; // Initial time in seconds (25 minutes)
  
    const formatTime = (time: number) => {
      const minutes = Math.floor(time / 60).toString().padStart(2, '0');
      const seconds = (time % 60).toString().padStart(2, '0');
      return `${minutes}:${seconds}`;
    };
  
    const startTimer = () => {
      isRunning = true;
      timerInterval = setInterval(() => {
        if (time > 0) {
          time--;
        } else {
          stopTimer();
          alert('Time is up!');
          audio.play();
        }
      }, 1000);
    };
  
    const stopTimer = () => {
      isRunning = false;
      clearInterval(timerInterval);
    };
  
    const resetTimer = () => {
      stopTimer();
      time = setTime;
    };
  
    onMount(() => {
      time = setTime;
    });
  
    onDestroy(() => {
      stopTimer();
    });
  </script>
  
  <style>
    .time-label {
      @apply flex items-center justify-center rounded-full h-32 w-32 text-4xl font-bold bg-blue-500 text-white;
    }
  </style>

  <div class="flex flex-col items-center justify-center h-screen gap-5">
    <h1 class="h1">Timer</h1>
    <div class="card p-4">
      <input  class="bg-transparent rounded-lg font-bold text-lg" type="number" bind:value={setTime} min="1" step="1" />
      <button class="btn variant-filled" on:click={resetTimer}>Set Time</button>
    </div>
    <div class="time-label">{formatTime(time)}</div>
    <div>
      {#if !isRunning}
        <button class="btn variant-filled" on:click={startTimer}>Start</button>
      {:else}
        <button class="btn variant-filled-secondary" on:click={stopTimer}>Stop</button>
      {/if}
    </div>
  </div>

  <audio src="sounds/alarm-clock.mp3" bind:this={audio}></audio>