<template>
  <div>
    <main>
      <Nuxt />
    </main>
  </div>
</template>
<style>
:root {
  --primary-color: #00c58e;
}

body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto,
    Helvetica Neue, Arial, Noto Sans, sans-serif, Apple Color Emoji,
    Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji;
  margin: 0;
}

a,
a:visited {
  color: var(--primary-color);
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

main {
  margin: 0 auto;
  padding: 0 1rem;
  margin-top: 40px;
  max-width: 1280px;
  text-align: center;
}

img {
  margin-bottom: 1rem;
}

li {
  margin: 0 0.5rem;
  padding: 0.25rem;
  font-size: 1rem;
}

nav {
  padding: 0 1rem;
}
button,
.button {
  background: var(--primary-color);
  padding: 0.75rem 1.5rem;
  outline: none;
  border-radius: 0.5rem;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  color: white;
  font-weight: 500;
  text-transform: uppercase;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  letter-spacing: 0.5px;
  margin: 0 0.5rem;
}

button:hover,
.button:hover {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  opacity: 0.8;
}

.txtSearch{
    height: 42px;
    min-width: 250px;
}
.result-error{
  border-radius:5px;
  padding:15px;
  border:1px solid rgba(255,0,0,1);
  background:rgba(255,0,0,0.2);
}

.author-list-holder, .work-list-holder, .work-info-holder{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-top:15px;
}
.author-list-item, .work-list-item, .work-info-holder{
    padding: 10px;
    border: 2px dashed;
    margin-bottom: 15px;
    text-align: left;
}
.author-list-item, .work-list-item{
  width: 30%;
}

.cover-img{width:35%}
.work-details{width:65%}

button.small-btn{
    padding: 0.5rem 1rem;
    font-size: 0.8rem;
}
</style>
