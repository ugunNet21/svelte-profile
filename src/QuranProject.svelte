<script>
  import { onMount } from 'svelte';

  let suratList = []; // Menyimpan daftar surat
  let filteredSuratList = []; // Menyimpan daftar surat yang difilter
  let selectedSurat = null; // Menyimpan surat yang dipilih
  let tafsirData = null; // Menyimpan data tafsir
  let searchQuery = ''; // Menyimpan query pencarian

  // Fungsi untuk mengambil daftar surat
  async function fetchSuratList() {
    try {
      const response = await fetch('https://equran.id/api/v2/surat');
      const data = await response.json();
      suratList = data.data;
      filteredSuratList = suratList; // Set filtered list sama dengan semua surat
    } catch (error) {
      console.error('Error fetching surat list:', error);
    }
  }

  // Fungsi untuk mengambil detail dan tafsir surat
  async function fetchTafsir(nomor) {
    try {
      const response = await fetch(`https://equran.id/api/v2/tafsir/${nomor}`);
      const data = await response.json();
      tafsirData = data.data;
    } catch (error) {
      console.error('Error fetching tafsir:', error);
    }
  }

  // Fungsi untuk memilih surat
  function selectSurat(surat) {
    selectedSurat = surat;
    fetchTafsir(surat.nomor);
  }

  // Fungsi untuk mencari surat
  function searchSurat() {
    filteredSuratList = suratList.filter(
      (surat) =>
        surat.namaLatin.toLowerCase().includes(searchQuery.toLowerCase()) ||
        surat.nomor.toString().includes(searchQuery)
    );
  }

  // Mengambil daftar surat saat komponen dimuat
  onMount(() => {
    fetchSuratList();
  });
</script>

<style>
  .quran-project {
    display: flex;
    gap: 20px;
    margin-top: 40px;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .surat-list-container {
    flex: 1;
    max-width: 300px;
  }

  .search-box {
    margin-bottom: 20px;
  }

  .search-box input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 8px;
    font-size: 1rem;
  }

  .surat-list {
    max-height: 600px;
    overflow-y: auto;
  }

  .surat-item {
    padding: 10px;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    transition: transform 0.2s;
    margin-bottom: 10px;
  }

  .surat-item:hover {
    transform: translateY(-5px);
  }

  .surat-item h3 {
    font-size: 1.2rem;
    color: #0077b5;
    margin: 0;
  }

  .surat-item p {
    font-size: 0.9rem;
    color: #555;
    margin: 5px 0;
  }

  .detail-section {
    flex: 2;
  }

  .detail-section h2 {
    font-size: 2rem;
    color: #333;
    margin-bottom: 20px;
  }

  .arabic-text {
    font-size: 1.5rem;
    text-align: right;
    margin-bottom: 20px;
    color: #333;
  }

  .tafsir-section {
    margin-top: 20px;
  }

  .tafsir-section h3 {
    font-size: 1.5rem;
    color: #333;
    margin-bottom: 10px;
  }

  .tafsir-section p {
    font-size: 1rem;
    color: #555;
    line-height: 1.5;
  }

  .audio-section {
    margin-top: 20px;
  }

  .audio-section h4 {
    font-size: 1.2rem;
    color: #333;
    margin-bottom: 10px;
  }

  .audio-section audio {
    width: 100%;
    margin-bottom: 10px;
  }

  @media (max-width: 768px) {
    .quran-project {
      flex-direction: column;
    }

    .surat-list-container {
      max-width: 100%;
    }
  }
</style>

<div class="quran-project">
  <!-- Daftar Surat dan Pencarian -->
  <div class="surat-list-container">
    <div class="search-box">
      <input
        type="text"
        placeholder="Cari surat..."
        bind:value={searchQuery}
        on:input={searchSurat}
      />
    </div>
    <div class="surat-list">
      {#each filteredSuratList as surat}
        <div class="surat-item" on:click={() => selectSurat(surat)}>
          <h3>{surat.namaLatin}</h3>
          <p>Nomor: {surat.nomor}</p>
          <p>Jumlah Ayat: {surat.jumlahAyat}</p>
        </div>
      {/each}
    </div>
  </div>

  <!-- Detail Surat -->
  {#if selectedSurat}
    <div class="detail-section">
      <h2>{selectedSurat.namaLatin}</h2>
      <div class="arabic-text">{selectedSurat.nama}</div>
      <p><strong>Arti:</strong> {selectedSurat.arti}</p>
      <p><strong>Tempat Turun:</strong> {selectedSurat.tempatTurun}</p>
      <p><strong>Deskripsi:</strong> {@html selectedSurat.deskripsi}</p>

      {#if tafsirData}
        <div class="tafsir-section">
          <h3>Tafsir:</h3>
          {#each tafsirData.tafsir as tafsir}
            <p><strong>Ayat {tafsir.ayat}:</strong> {@html tafsir.teks}</p>
          {/each}
        </div>
      {/if}

      <div class="audio-section">
        <h4>Audio Surat:</h4>
        {#each Object.entries(selectedSurat.audioFull) as [key, audioUrl]}
          <audio controls>
            <source src={audioUrl} type="audio/mpeg" />
            Browser Anda tidak mendukung elemen audio.
          </audio>
        {/each}
      </div>
    </div>
  {/if}
</div>