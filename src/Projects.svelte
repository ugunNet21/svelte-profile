<script>
  const projects = [
    {
      name: "Project 1",
      description: "A web app for managing tasks.",
      link: "https://example.com",
    },
    {
      name: "Project 2",
      description: "A portfolio website built with Svelte.",
      link: "https://example.com",
    },
    {
      name: "Project 3",
      description: "An e-commerce platform using React.",
      link: "https://example.com",
    },
  ];
</script>

<div class="projects">
  <h2>Projects</h2>
  <div class="projects-list">
    {#each projects as project}
      <div class="project">
        <h3>{project.name}</h3>
        <p>{project.description}</p>
        <a href={project.link} target="_blank" class="project-link">View Project</a>
      </div>
    {/each}
  </div>
</div>

<style>
  .projects {
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

  .projects-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
  }

  .project {
    background-color: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  h3 {
    font-size: 1.5rem;
    color: #0077b5;
    margin: 0 0 10px;
  }

  .project-link {
    display: inline-block;
    margin-top: 10px;
    color: #0077b5;
    text-decoration: none;
    font-weight: bold;
  }

  @media (max-width: 768px) {
    .projects-list {
      grid-template-columns: 1fr;
    }
  }
</style>