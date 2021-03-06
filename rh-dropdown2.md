---
layout: component
---

<script>require(['/assets/node_modules/@rhelements/rh-dropdown/rh-dropdown.compiled.js'])</script>
<noscript>
  <style>
    rh-dropdown:not([defined]) {
      opacity: 1;
    }
  </style>
</noscript>

<style>
section { margin-top: 1.5em; }
</style>

# Tacos

<rh-dropdown>
  <rh-dropdown-button no-aria-haspopup="true">
    <h2>Tacos types</h2>
  </rh-dropdown-button>
  <rh-dropdown-menu>
    <ul>
      <li><a href="#al-pastor">Al Pastor</a></li>
      <li><a href="#carnitas">Carnitas</a></li>
      <li><a href="#carne-asada">Carne Asada</a></li>
      <li><a href="#fish">Fish</a></li>
    </ul>
  </rh-dropdown-menu>
</rh-dropdown>

<section id="al-pastor">
  <h2>Al pastor</h2>
  <p>Al pastor (from Spanish, "shepherd style"), also known as tacos al pastor, is a dish developed in Central Mexico that is based on shawarma spit-grilled meat brought by the Lebanese immigrants to Mexico.</p>
  <p><cite><a href="https://en.wikipedia.org/wiki/Al_pastor">Al pastor, from Wikipedia, the free encyclopedia</a></cite></p>
</section>

<section id="carnitas">
  <h2>Carnitas</h2>
  <p>Carnitas, literally meaning "little meats", is a dish of Mexican cuisine originating from the state of Michoacán. Carnitas are made by braising or simmering pork in oil or preferably lard until tender. The process takes three to four hours, and the result is very tender and juicy meat, which is then typically served with chopped coriander leaves (cilantro) and diced onion, salsa, guacamole, tortillas, and refried beans (frijoles refritos).</p>
  <p><cite><a href="https://en.wikipedia.org/wiki/Carnitas">Carnitas, from Wikipedia, the free encyclopedia</a></cite></p>
</section>

<section id="carne-asada">
  <h2>Carne Asada</h2>
  <p>Carne asada (literally "flesh/meat/beef" "roast/broiled/grilled") is a Latin American dish of grilled and sliced beef, usually sirloin steak, tenderloin steak or rib steak. It is usually cooked with a certain amount of searing to impart a charred flavor. Carne asada can be served as a main dish or as an ingredient in other dishes. The term carne asada translates to "grilled meat"; the English "roast beef" is so named in Spanish.</p>
  <p><cite><a href="https://en.wikipedia.org/wiki/Carne_asada">Carne Asada, from Wikipedia, the free encyclopedia</a></cite></p>
</section>

<section id="fish">
  <h2>Fish tacos</h2>
  <p>Tacos de pescado ("fish tacos") originated in Baja California in Mexico, where they consist of grilled or fried fish, lettuce or cabbage, pico de gallo, and a sour cream or citrus/mayonnaise sauce, all placed on top of a corn or flour tortilla. In the United States, they were first popularized by the Rubio's fast-food chain, and remain most popular in California, Colorado, and Washington. In California, they are often found at street vendors, and a regional variation is to serve them with cabbage and coleslaw dressing on top.</p>
  <p><cite><a href="https://en.wikipedia.org/wiki/Taco#Traditional_tacos">Traditional tacos, from Wikipedia, the free encyclopedia</a></cite></p>
</section>
