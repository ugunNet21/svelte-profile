<script>
    export let name = "Gugun Gunawan, S.Kom";
    export let avatar = "https://careergunawan.my.id/frontend/assets/images/about-banner1.gif";
    export let bio = "Software Engineer at XYZ. Passionate about coding and design.";
  </script>
  
  <div class="profile">
    <img src={avatar} alt={name} class="avatar" />
    <div class="info">
      <h1>{name}</h1>
      <p class="bio">{bio}</p>
      <div class="social-links">
        <a href="https://github.com/ugunNet21" target="_blank">GitHub</a>
        <a href="https://www.linkedin.com/in/career-gunawan/" target="_blank">LinkedIn</a>
        <a href="https://twitter.com" target="_blank">Twitter</a>
      </div>
    </div>
  </div>
  
  <style>
    .profile {
      display: flex;
      align-items: center;
      flex-direction: column;
      text-align: center;
      padding: 20px;
      background-color: #f9f9f9;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
  
    .avatar {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      margin-bottom: 20px;
      object-fit: cover; /* Untuk memastikan gambar terlihat proporsional */
    }
  
    h1 {
      font-size: 2.5rem;
      margin: 0;
      color: #333;
    }
  
    .bio {
      font-size: 1.2rem;
      color: #666;
      margin: 10px 0;
    }
  
    .social-links {
      margin-top: 15px;
    }
  
    .social-links a {
      margin: 0 10px;
      text-decoration: none;
      color: #0077b5;
      font-weight: bold;
    }
  
    @media (min-width: 768px) {
      .profile {
        flex-direction: row;
        text-align: left;
      }
  
      .avatar {
        margin-right: 30px;
        margin-bottom: 0;
      }
    }
  </style>