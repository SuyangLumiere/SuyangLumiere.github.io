---
layout: page
permalink: /friends/
title: friends
description: Here are some of my friends
nav: true
nav_order: 6
---

<div id="friends-container" style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: center; margin-top: 20px;"></div>

<script>
// user id
const friendUsernames = [
  'YihDu',
  'Tzsha',
  'SuyangLumiere'
];

const container = document.getElementById('friends-container');

friendUsernames.forEach(username => {
  fetch(`https://api.github.com/users/${username}`)
    .then(response => response.json())
    .then(data => {
      if (data.message === "Not Found") return; 
      
      const name = data.name || data.login;
      const bio = data.bio || '这个人很懒，还没有写个性签名~';
      
      const cardHTML = `
        <div style="border: 1px solid var(--global-divider-color); border-radius: 10px; padding: 20px; width: 220px; text-align: center; background-color: var(--global-bg-color); box-shadow: 0 4px 6px rgba(0,0,0,0.1); transition: transform 0.2s;">
          <a href="${data.html_url}" target="_blank" style="text-decoration: none;">
            <img src="${data.avatar_url}" alt="${name}" style="border-radius: 50%; width: 100px; height: 100px; margin-bottom: 15px; object-fit: cover; border: 2px solid var(--global-theme-color);">
          </a>
          <h3 style="margin: 0; font-size: 1.2rem; color: var(--global-text-color);">
            <a href="${data.html_url}" target="_blank" style="text-decoration: none; color: inherit;">${name}</a>
          </h3>
          <p style="color: var(--global-text-color-light); font-size: 0.9rem; margin: 5px 0;">@${data.login}</p>
          <p style="font-size: 0.85rem; color: var(--global-text-color); margin-top: 10px; line-height: 1.4; display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden;">
            ${bio}
          </p>
        </div>
      `;
      container.innerHTML += cardHTML;
    })
    .catch(error => console.error('获取 GitHub 信息出错:', error));
});
</script>
