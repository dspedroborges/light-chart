# @light-chart/light-chart.js

Lightweight SVG charts with zero dependencies. Renders bar charts, line charts, and pie charts as inline SVG.

## Installation

```html
<script src="light-chart.min.js"></script>
```

## Size

- **minified:** ~3KB
- **compressed (tar.gz):** ~1.1KB

That's it. That's the whole library.

## Quick Start

```html
<div id="pie"></div>
<div id="bar"></div>
<div id="line"></div>

<script src="light-chart.min.js"></script>
<script>
  document.getElementById("pie").innerHTML = chart.pie({
    labels: ["A", "B", "C"],
    data: [10, 20, 30]
  });

  document.getElementById("bar").innerHTML = chart.bar({
    labels: ["Jan", "Feb", "Mar"],
    data: [5, 15, 25]
  });

  document.getElementById("line").innerHTML = chart.line({
    labels: ["Q1", "Q2", "Q3", "Q4"],
    data: [3, 12, 8, 20]
  });
</script>
```

---

## API

### chart.bar

Renders a vertical bar chart.

```javascript
chart.bar({
  labels: ["Jan", "Feb", "Mar"],
  data: [10, 20, 30]
});
```

### chart.line

Renders a line chart with data points.

```javascript
chart.line({
  labels: ["Q1", "Q2", "Q3", "Q4"],
  data: [3, 12, 8, 20]
});
```

### chart.pie

Renders a pie chart with automatic labeling.

```javascript
chart.pie({
  labels: ["Apple", "Banana", "Cherry"],
  data: [30, 45, 25]
});
```

**Options:**
- `labels` - Array of strings for x-axis labels
- `data` - Array of numbers

**Note:** Labels and data arrays must have the same length. Returns an empty string if they don't match.

---

## Server-Side Rendering with HTMX

You can render charts server-side and send the SVG to the client using HTMX.

### Server Example (Elysia + TSX)

```typescript
// server.ts
import { Elysia } from 'elysia';
import { chart } from './light-chart.js';

const app = new Elysia()
  .get('/chart/bar', () => chart.bar({
    labels: ["Jan", "Feb", "Mar"],
    data: [10, 20, 30]
  }))
  .get('/chart/line', () => chart.line({
    labels: ["Q1", "Q2", "Q3", "Q4"],
    data: [3, 12, 8, 20]
  }))
  .get('/chart/pie', () => chart.pie({
    labels: ["A", "B", "C"],
    data: [10, 20, 30]
  }))
  .listen(3000);

console.log(`Server running at http://localhost:${app.server?.port}`);
```

Run with `npx tsx server.ts`

### HTMX Client

```html
<div hx-get="/chart/bar" hx-trigger="load">
  Loading...
</div>
```

---

## Complete Examples

### Bar Chart

```html
<!DOCTYPE html>
<html>
<body>
  <h2>Monthly Sales</h2>
  <div id="bar-chart"></div>

  <script src="light-chart.min.js"></script>
  <script>
    document.getElementById("bar-chart").innerHTML = chart.bar({
      labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
      data: [120, 180, 90, 200, 150, 220]
    });
  </script>
</body>
</html>
```

### Line Chart

```html
<!DOCTYPE html>
<html>
<body>
  <h2>Website Traffic</h2>
  <div id="line-chart"></div>

  <script src="light-chart.min.js"></script>
  <script>
    document.getElementById("line-chart").innerHTML = chart.line({
      labels: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
      data: [150, 230, 180, 320, 290, 410, 380]
    });
  </script>
</body>
</html>
```

### Pie Chart

```html
<!DOCTYPE html>
<html>
<body>
  <h2>Market Share</h2>
  <div id="pie-chart"></div>

  <script src="light-chart.min.js"></script>
  <script>
    document.getElementById("pie-chart").innerHTML = chart.pie({
      labels: ["Product A", "Product B", "Product C", "Product D"],
      data: [35, 25, 20, 20]
    });
  </script>
</body>
</html>
```

### Dynamic Updates

```html
<!DOCTYPE html>
<html>
<body>
  <button onclick="updateChart()">Update Data</button>
  <div id="chart"></div>

  <script src="light-chart.min.js"></script>
  <script>
    const chartData = { labels: ["A", "B", "C"], data: [10, 20, 30] };
    
    function render() {
      document.getElementById("chart").innerHTML = chart.bar(chartData);
    }
    
    function updateChart() {
      chartData.data = chartData.data.map(() => Math.floor(Math.random() * 100));
      render();
    }
    
    render();
  </script>
</body>
</html>
```

### Multiple Charts

```html
<!DOCTYPE html>
<html>
<body>
  <table>
    <tr>
      <td><div id="sales"></div></td>
      <td><div id="revenue"></div></td>
    </tr>
    <tr>
      <td><div id="users"></div></td>
      <td><div id="distribution"></div></td>
    </tr>
  </table>

  <script src="light-chart.min.js"></script>
  <script>
    document.getElementById("sales").innerHTML = chart.bar({
      labels: ["Q1", "Q2", "Q3", "Q4"],
      data: [45, 52, 38, 60]
    });

    document.getElementById("revenue").innerHTML = chart.line({
      labels: ["Jan", "Feb", "Mar", "Apr"],
      data: [12, 19, 15, 25]
    });

    document.getElementById("users").innerHTML = chart.line({
      labels: ["Week 1", "Week 2", "Week 3", "Week 4"],
      data: [100, 250, 400, 380]
    });

    document.getElementById("distribution").innerHTML = chart.pie({
      labels: ["North", "South", "East", "West"],
      data: [30, 25, 25, 20]
    });
  </script>
</body>
</html>
```

---

## Browser Support

Any modern browser with SVG support. Chrome, Firefox, Safari, Edge all work.

## License

MIT
