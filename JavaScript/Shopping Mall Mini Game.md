# HTML
<details>
<summary>game.html</summary>
<div markdown="1">

```
<body>
    <!-- Logo -->
    <img src="imgs/logo.png" alt="Logo" class="logo" />

    <!-- Buttons -->
    <section class="buttons">
      <button class="btn">
        <img
          src="imgs/blue_t.png"
          alt="tshirt"
          class="imgBtn"
          data-key="type"
          data-value="tshirt"
        />
      </button>
      <button class="btn">
        <img
          src="imgs/blue_p.png"
          alt="pants"
          class="imgBtn"
          data-key="type"
          data-value="pants"
        />
      </button>
      <button class="btn">
        <img
          src="imgs/blue_s.png"
          alt="skirt"
          class="imgBtn"
          data-key="type"
          data-value="skirt"
        />
      </button>
      <button class="btn colorBtn blue" data-key="color" data-value="blue">
        Blue
      </button>
      <button class="btn colorBtn yellow" data-key="color" data-value="yellow">
        Yellow
      </button>
      <button class="btn colorBtn pink" data-key="color" data-value="pink">
        Pink
      </button>
    </section>

    <!-- Items -->
    <ul class="items">
        <li class="item">
          <img src="imgs/blue_t.png" alt="tshirt" class="item__thumbnail">
          <span class="item__description">male, large</span>
        </li>

        <li class="item">
          <img src="imgs/blue_s.png" alt="skirt" class="item__thumbnail">
          <span class="item__description">female, small</span>
        </li>

        <li class="item">
          <img src="imgs/blue_p.png" alt="pants" class="item__thumbnail">
          <span class="item__description">male, large</span>
        </li>

        <li class="item">
          <img src="imgs/pink_t.png" alt="tshirt" class="item__thumbnail">
          <span class="item__description">female, small</span>
        </li>

        <li class="item">
          <img src="imgs/pink_s.png" alt="skirt" class="item__thumbnail">
          <span class="item__description">female, large</span>
        </li>

        <li class="item">
          <img src="imgs/pink_p.png" alt="pants" class="item__thumbnail">
          <span class="item__description">male, large</span>
        </li>
        
        <li class="item">
          <img src="imgs/yellow_t.png" alt="tshirt" class="item__thumbnail">
          <span class="item__description">female, small</span>
        </li>
        
        <li class="item">
          <img src="imgs/yellow_s.png" alt="skirt" class="item__thumbnail">
          <span class="item__description">female, small</span>
        </li>
        
        <li class="item">
          <img src="imgs/yellow_p.png" alt="pants" class="item__thumbnail">
          <span class="item__description">male, large</span>
        </li>

    </ul>
  </body>
```
</div>
</details>

# CSS
<details>
<summary>game.css</summary>
<div markdown="1">

```
:root {
    /* color */
    --color-black: #3f454d;
    --color-white: #ffffff;
    --color-blue: #3b88c3;
    --color-yellow: #fbbe28;
    --color-pink: #fd7f84;
    --color-light-grey: #dfdfdf;
  
    /* size */
    --base-space: 8px;
    --size-button: 60px;
    --size-border: 4px;
    --size-thumbnail: 50px;
    --font-size: 18px;
  
    /* annimation */
    --animation: 300ms;
  }

/* body */
  body {
    height: 100vh;
    background-color: var(--color-black);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

/* logo */
  .logo {
    cursor: pointer;
    transition: transform var(--animation) ease;
  }

/* button */
  .btn {
    background-color: transparent;
    border: none;
    outline: none;
    cursor: pointer;
    transition: transform var(--animation) ease;
    margin-right: var(--base-space);
  }
  
  .btn:hover,
  .logo:hover {
    transform: scale(1.1);
  }
  
  .buttons {
    display: flex;
    align-items: center;
  }
  
  .imgBtn {
    width: var(--size-button);
    height: var(--size-button);
  }
  
  .colorBtn {
    font-size: var(--font-size);
    padding: calc(var(--base-space) * 2);
    border-radius: var(--size-border);
  }
  
  .blue {
    background-color: var(--color-blue);
  }
  
  .yellow {
    background-color: var(--color-yellow);
  }
  
  .pink {
    background-color: var(--color-pink);
  }

/* items */
  .items {
    width: 60%;
    height: 60%;
    list-style: none;
    padding-left: 0;
  }
  
  .item {
    background-color: var(--color-white);
    display: flex;
    align-items: center;
    padding: var(--base-space);
    margin-bottom: var(--base-space);
  }
  
  .item.invisible {
    background-color: var(--color-white);
    display: none;
  }
  
  .item__thumbnail {
    width: var(--size-thumbnail);
    height: var(--size-thumbnail);
  }
  
  .item__description {
    margin-left: var(--base-space);
    font-size: var(--font-size);
  }
  
```
</div>
</details>

## HTML & CSS 완성
![html css](https://user-images.githubusercontent.com/73509513/159412737-9ffc5700-234d-43e4-a291-ec7880ba73cc.PNG)

# JavaScript
<details>
<summary>game.js</summary>
<div markdown="1">

```
 
```

</div>
</details>

## JS 완성
