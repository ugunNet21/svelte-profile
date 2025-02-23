<script>
  const skills = [
    "JavaScript",
    "Svelte",
    "React",
    "Node.js",
    "CSS",
    "HTML",
    "Git",
    "Python",
    "TypeScript",
    "Express",
    "MongoDB",
    "SQL",
    "PostgreSQL",
    "MySQL",
    "Docker",
    "Kubernetes",
    "AWS",
    "Azure",
    "Google Cloud",
    "Laravel",
    "Flutter"
  ];
</script>

<div class="skills">
  <h2>Skills</h2>
  <div class="skills-list">
    {#each skills as skill}
      <span class="skill">{skill}</span>
    {/each}
  </div>
</div>

<style>
  .skills {
    margin-top: 40px;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  h2 {
    font-size: 2rem;
    color: #333;
    margin-bottom: 20px;
  }

  .skills-list {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .skill {
    background-color: #0077b5;
    color: white;
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 0.9rem;
  }

  @media (max-width: 768px) {
    .skills-list {
      justify-content: center;
    }
  }
</style>