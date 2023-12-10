<script>
    export let match;
  
    const getTeamColor = (alliance, teamNumber) => {
      return alliance === 'red' ? 'red' : 'blue';
    };
  </script>
  
  <main>
    <div class="match-card">
      <h3>Match {match.comp_level.toUpperCase()} {match.set_number} - {match.match_number}</h3>
      
      <div class="match-info">
        <p>Match Day: {new Date(match.time * 1000).toLocaleDateString()}</p>
        <p>Match Time: {new Date(match.time * 1000).toLocaleTimeString()}</p>
      </div>
  
      <div class="alliance-video-container">
        <div class="alliance-container">
          <div class="alliance red">
            <h4>Red Alliance</h4>
            <div class="team">
              <p>Team {match.red_1}</p>
              <p>Auto Score: {match.red_auto_epa_sum}</p>
              <p>Teleop Score: {match.red_teleop_epa_sum}</p>
              <p>Endgame Score: {match.red_endgame_epa_sum}</p>
              <p>Fouls: {match.red_fouls}</p>
              <p>Total Score: {match.red_score}</p>
              <p>Net EPA: {match.red_epa_sum}</p>
            </div>

          </div>
  
          <div class="alliance blue">
            <h4>Blue Alliance</h4>
            <div class="team">
              <p>Team {match.blue_1}</p>
              <p>Auto Score: {match.blue_auto_epa_sum}</p>
              <p>Teleop Score: {match.blue_teleop_epa_sum}</p>
              <p>Endgame Score: {match.blue_endgame_epa_sum}</p>
              <p>Fouls: {match.blue_fouls}</p>
              <p>Total Score: {match.blue_score}</p>
              <p>Net EPA: {match.blue_epa_sum}</p>
            </div>
          </div>
        </div>
  
        <div class="video">
          <iframe src={`https://www.youtube.com/embed/${match.video}`} frameborder="0" allowfullscreen loading="lazy" title="video"></iframe>
        </div>
      </div>
    </div>
  </main>
  
  <style>

    main {
      text-align: center;
      margin-top: 20px;
    }
  
    .match-card {
      display: flex;
      flex-direction: column;
      align-items: center;
      border: 1px solid #ccc;
      padding: 10px;
      margin: 10px;
    }
  
    .match-info {
      margin-bottom: 10px;
    }
  
    .alliance-video-container {
      display: flex;
      justify-content: space-between;
      width: 100%;
      margin-bottom: 10px;
    }
  
    .alliance-container {
      display: flex;
      justify-content: space-between;
      width: 48%;
    }
  
    .alliance {
      width: 48%;
      padding: 10px;
      border: 1px solid #eee;
      margin: 5px;
    }
  
    .team {
      margin-top: 10px;
    }
  
    .red {
      background-color: #ff9999;
    }
  
    .blue {
      background-color: #99ccff;
    }
  
    .video {
      width: 48%;
    }
  
    iframe {
      width: 100%;
      height: 400px; 
    }
  </style>
  