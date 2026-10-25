# MITHINKUMAR-S
My first repository on GitHub

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#123c35">
  <title>LocalFind AI | Find local businesses</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0; font-family: Arial, sans-serif;
      background: #f4f7f5; color: #18352e;
    }
    header {
      background: #123c35; color: white;
      padding: 26px 18px; text-align: center;
    }
    header h1 { margin: 0 0 8px; }
    main { max-width: 760px; margin: auto; padding: 18px; }
    input, select {
      width: 100%; padding: 13px; margin: 7px 0;
      border: 1px solid #c8d5ce; border-radius: 10px;
      font-size: 16px; background: white;
    }
    .notice { font-size: 13px; color: #725c2a; }
    .shop {
      background: white; border-radius: 14px;
      padding: 16px; margin: 12px 0;
      box-shadow: 0 2px 10px #163c3510;
    }
    .shop h3 { margin: 0 0 8px; }
    .tag { font-size: 13px; color: #53685e; }
    a { color: #08765b; margin-right: 12px; }
    footer { text-align: center; padding: 24px; color: #60736a; }
  </style>
</head>
<body>
  <header>
    <h1>LocalFind AI</h1>
    <div>உங்கள் ஊர் கடைகள் — Your town, all in one place</div>
  </header>

  <main>
    <h2>Find what you need</h2>
    <input id="search" placeholder="Search / தேடுங்கள்: photo frame, tailor..."
      aria-label="Search local businesses">
    <select id="category" aria-label="Business category">
      <option value="">All categories</option>
      <option>Photography</option>
      <option>Clothing</option>
      <option>Food</option>
      <option>Repair</option>
    </select>
    <p class="notice">
      Demo only: listings are examples, not verified local businesses.
    </p>
    <section id="results" aria-live="polite"></section>
  </main>

  <footer>LocalFind AI · Discover local. Shop local.</footer>

  <script>
    // Replace these examples with businesses that have agreed to be listed.
    const shops = [
      {
        name: "Sample Photo & Frame Shop",
        category: "Photography",
        services: "photo printing, photo frame, passport photo",
        area: "Sample area",
        phone: "",
        map: "https://www.google.com/maps/search/?api=1&query=photo+frame+shop+Paravakkottai"
      },
      {
        name: "Sample Clothing Store",
        category: "Clothing",
        services: "shirts, trousers, tailoring",
        area: "Sample area",
        phone: "",
        map: "https://www.google.com/maps/search/?api=1&query=clothing+shop+Paravakkottai"
      },
      {
        name: "Sample Food Shop",
        category: "Food",
        services: "snacks, tea, takeaway",
        area: "Sample area",
        phone: "",
        map: "https://www.google.com/maps/search/?api=1&query=food+shop+Paravakkottai"
      }
    ];

    const search = document.getElementById("search");
    const category = document.getElementById("category");
    const results = document.getElementById("results");

    function render() {
      const q = search.value.trim().toLowerCase();
      const cat = category.value;

      const matches = shops.filter(shop => {
        const text = [
          shop.name, shop.category, shop.services, shop.area
        ].join(" ").toLowerCase();

        return text.includes(q) &&
          (!cat || shop.category === cat);
      });

      results.replaceChildren();

      if (!matches.length) {
        results.textContent =
          "No matching shops yet. Try another search.";
        return;
      }

      matches.forEach(shop => {
        const card = document.createElement("article");
        card.className = "shop";

        const title = document.createElement("h3");
        title.textContent = shop.name;

        const details = document.createElement("p");
        details.textContent =
          shop.category + " · " + shop.area;

        const services = document.createElement("p");
        services.textContent = shop.services;

        card.append(title, details, services);

        const map = document.createElement("a");
        map.href = shop.map;
        map.target = "_blank";
        map.rel = "noopener";
        map.textContent = "View map";
        card.append(map);

        if (shop.phone) {
          const call = document.createElement("a");
          call.href = "tel:" + shop.phone;
          call.textContent = "Call";

          const wa = document.createElement("a");
          wa.href = "https://wa.me/" +
            shop.phone.replace(/\D/g, "");
          wa.target = "_blank";
          wa.rel = "noopener";
          wa.textContent = "WhatsApp";

          card.append(call, wa);
        }

        results.append(card);
      });
    }

    search.addEventListener("input", render);
    category.addEventListener("change", render);
    render();
  </script>
</body>
</html>
ś
