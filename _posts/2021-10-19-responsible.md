---
layout: post
title: レスポンシブル対応
---

```scss
@media (max-width: 40rem) {

  header {
    height: 100%;
    .header-items {
      margin: 0 $spacing-1;
      h1 {
        padding-top: $spacing-4;
      }
      h2 {
        font-size: $fontSize-3;
      }
      .header-icons {
        padding-bottom: $spacing-2;
      }
    }
  }

  main, footer {
    margin: 0;
    padding: 0 $spacing-1;
  }

  img {
    width: 100%;
    display: block;
    margin: 0 auto;
  }
}
```