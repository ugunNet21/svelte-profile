<script>
	import Profile from './Profile.svelte';
	import Projects from './Projects.svelte';
	import Skills from './Skills.svelte';
  </script>
  
  <main>
	<Profile
	  name="Gugun Gunawan, S.Kom"
	  avatar="https://careergunawan.my.id/frontend/assets/images/about-banner1.gif"
	  bio="Software Engineer at XYZ. Passionate about coding and design."
	/>
	<Skills />
	<Projects />
  </main>
  
  <style>
	main {
	  font-family: 'Arial', sans-serif;
	  max-width: 1200px;
	  margin: 0 auto;
	  padding: 20px;
	}
  
	@media (max-width: 768px) {
	  main {
		padding: 10px;
	  }
	}
  </style>