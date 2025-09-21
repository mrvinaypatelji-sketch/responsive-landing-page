# responsive-landing-page
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Fixed Interactive Navigation</title>
  <style>
    /* Basic reset */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    html,body { height: 100%; font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial; }

    /* Fixed nav container */
    .site-nav {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      height: 68px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 20px;
      z-index: 9999;
      transition: background-color 250ms ease, color 250ms ease, height 250ms ease, box-shadow 250ms ease;
      background: rgba(33, 150, 243, 0.12); /* semi-transparent default */
      color: #08304a;
      backdrop-filter: blur(4px);
    }

    /* Nav when page is scrolled */
    .site-nav.scrolled {
      background: linear-gradient(90deg,#0f4c81,#1976d2);
      color: #fff;
      box-shadow: 0 6px 20px rgba(10,20,40,0.25);
      height: 58px;
    }

    .brand {
      display: flex;
      gap: 10px;
      align-items: center;
      font-weight: 700;
      letter-spacing: 0.2px;
    }
    .brand .logo {
      width: 36px;
      height: 36px;
      border-radius: 6px;
      background: linear-gradient(135deg,#ffd54f,#ff8a65);
      display: inline-block;
    }

    /* Menu */
    .menu {
      display: flex;
      gap: 14px;
      align-items: center;
      list-style: none;
    }
    .menu a {
      display: inline-block;
      padding: 8px 12px;
      border-radius: 8px;
      text-decoration: none;
      color: inherit;
      font-weight: 600;
      transition: transform 140ms ease, background-color 160ms ease, color 160ms ease, box-shadow 160ms ease;
      outline: none;
    }

    /* Hover / focus styles (visible regardless of scrolled or not) */
    .menu a:hover,
    .menu a:focus {
      transform: translateY(-3px);
      box-shadow: 0 6px 18px rgba(0,0,0,0.12);
      background: rgba(255,255,255,0.12);
    }

    /* When nav is scrolled, change hover accent */
    .site-nav.scrolled .menu a:hover,
    .site-nav.scrolled .menu a:focus {
      background: rgba(255,255,255,0.14);
      color: #fff;
    }

    /* Active item state (can be set by JS when clicked) */
    .menu a.active {
      background: rgba(0,0,0,0.12);
      color: #fff;
      box-shadow: inset 0 -3px 0 rgba(255,255,255,0.14);
    }
    .site-nav.scrolled .menu a.active {
      background: rgba(255,255,255,0.12);
      color: #072b44;
      box-shadow: inset 0 -3px 0 rgba(7,43,68,0.08);
    }

    /* Mobile: collapse into a simple hamburger */
    @media (max-width: 720px) {
      .menu { display: none; }
      .hamburger { display: inline-flex; align-items:center; gap:8px; }
      .hamburger button {
        background: transparent;
        border: none;
        padding: 8px;
        cursor: pointer;
        font-size: 18px;
        color: inherit;
      }

      /* simple dropdown when opened */
      .menu.mobile-open {
        position: fixed;
        top: 68px;
        right: 12px;
        background: rgba(255,255,255,0.96);
        border-radius: 12px;
        padding: 12px;
        display: flex;
        flex-direction: column;
        gap: 6px;
        box-shadow: 0 8px 30px rgba(10,20,40,0.15);
      }
      .site-nav.scrolled .menu.mobile-open {
        background: rgba(12,32,64,0.95);
        color: #fff;
      }
    }

    /* Page content so you can scroll */
    main {
      padding-top: 92px; /* space for fixed nav */
      max-width: 1000px;
      margin: 0 auto;
      padding-left: 18px;
      padding-right: 18px;
      line-height: 1.6;
    }
    section {
      margin: 28px 0;
      background: linear-gradient(180deg,#ffffff, #f6fbff);
      padding: 28px;
      border-radius: 12px;
      box-shadow: 0 8px 30px rgba(10,20,40,0.03);
    }
    h1 { margin-bottom: 12px; font-size: 28px; }
  </style>
</head>
<body>
  <nav class="site-nav" id="siteNav" aria-label="Main navigation">
    <div class="brand" aria-hidden="true">
      <span class="logo" role="img" aria-label="logo"></span>
      <span>MySite</span>
    </div>

    <!-- Desktop menu -->
    <ul class="menu" id="mainMenu" role="menubar">
      <li role="none"><a href="#home" role="menuitem" data-target="home">Home</a></li>
      <li role="none"><a href="#about" role="menuitem" data-target="about">About</a></li>
      <li role="none"><a href="#services" role="menuitem" data-target="services">Services</a></li>
      <li role="none"><a href="#contact" role="menuitem" data-target="contact">Contact</a></li>
    </ul>

    <!-- Simple hamburger for mobile (JS toggles menu.mobile-open) -->
    <div class="hamburger" aria-hidden="false">
      <button id="hambtn" aria-expanded="false" aria-controls="mainMenu" aria-label="Open menu">☰</button>
    </div>
  </nav>

  <main>
    <!-- Long content to demonstrate scrolling -->
    <section id="home">
      <h1>Home</h1>
      <p>Welcome — scroll down to see the navigation change its style. Hover over menu items to see hover interactions. Clicking a menu item will set it active.</p>
      <p>Repeat content to create scroll length.</p>
    </section>

    <section id="about">
      <h1>About</h1>
      <p>About content. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse vitae.</p>
    </section>

    <section id="services">
      <h1>Services</h1>
      <p>Services content. Sed euismod, arcu vitae laoreet lacinia, mi libero faucibus lacus, vitae convallis massa.</p>
    </section>

    <section id="contact">
      <h1>Contact</h1>
      <p>Contact content. Phone, email, etc.</p>
    </section>

    <!-- filler -->
    <section>
      <h1>More content</h1>
      <p>Scrolling example — more text below to extend the page.</p>
      <p style="margin-top:14px;">(You can copy-paste this section several times when testing.)</p>
    </section>
  </main>

  <script>
    (function () {
      const nav = document.getElementById('siteNav');
      const threshold = 40; // px scrolled before we change nav style
      const links = document.querySelectorAll('.menu a');
      const hamBtn = document.getElementById('hambtn');
      const menu = document.getElementById('mainMenu');

      // Add / remove .scrolled on scroll
      function onScroll() {
        if (window.scrollY > threshold) {
          nav.classList.add('scrolled');
        } else {
          nav.classList.remove('scrolled');
        }
      }

      // Throttle scroll handler for performance (simple)
      let ticking = false;
      window.addEventListener('scroll', function () {
        if (!ticking) {
          window.requestAnimationFrame(function () {
            onScroll();
            ticking = false;
          });
          ticking = true;
        }
      }, { passive: true });

      // Set active link on click and smooth-scroll to section
      links.forEach(a => {
        a.addEventListener('click', function (e) {
          // manage active class
          links.forEach(x => x.classList.remove('active'));
          this.classList.add('active');

          // smooth scroll to section (native)
          const targetId = this.getAttribute('href').replace('#','');
          const target = document.getElementById(targetId);
          if (target) {
            e.preventDefault();
            window.scrollTo({
              top: target.getBoundingClientRect().top + window.pageYOffset - (nav.offsetHeight + 8),
              behavior: 'smooth'
            });
            // close mobile menu (if open)
            if (menu.classList.contains('mobile-open')) {
              menu.classList.remove('mobile-open');
              hamBtn.setAttribute('aria-expanded', 'false');
            }
          }
        });

        // keyboard accessibility: add focus visible styles via :focus in CSS; ensure keyboard users can tab
        a.addEventListener('keydown', function (e) {
          if (e.key === 'Enter' || e.key === ' ') {
            this.click();
          }
        });
      });

      // Mobile hamburger toggle
      hamBtn.addEventListener('click', function () {
        const expanded = this.getAttribute('aria-expanded') === 'true';
        if (expanded) {
          menu.classList.remove('mobile-open');
          this.setAttribute('aria-expanded', 'false');
        } else {
          menu.classList.add('mobile-open');
          this.setAttribute('aria-expanded', 'true');
        }
      });

      // Optional: set active link when section is in view (IntersectionObserver)
      const observerOptions = { root: null, rootMargin: '-40% 0px -40% 0px', threshold: 0 };
      const sections = document.querySelectorAll('main section[id]');
      const io = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const id = entry.target.id;
            links.forEach(a => {
              a.classList.toggle('active', a.getAttribute('href') === '#' + id);
            });
          }
        });
      }, observerOptions);
      sections.forEach(s => io.observe(s));

      // initial check on load
      onScroll();
    })();
  </script>
</body>
</html>
