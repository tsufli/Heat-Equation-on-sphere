# Heat Kernel on the Sphere

Interactive simulation of the heat equation `u_t = Δu` on the unit 2-sphere. Click the sphere to place a delta function of heat and watch it diffuse in real time. Click again (and again) to add more sources.

## How it works

The heat kernel on S² is the exact solution for an initial delta at point `p`:

```
K(t, x, p) = Σ_l (2l+1)/(4π) · e^{-l(l+1)t} · P_l(x·p)
```

where `P_l` are Legendre polynomials (evaluated with the stable three-term recurrence). Because the equation is linear, multiple clicks are just a sum of kernels, each with its own start time. No time-stepping is used, so the solution is exact (up to series truncation) at any speed.

Each source starts at a small age `T0 = 0.004`, so it's a very narrow bump rather than an infinitely sharp delta. The number of series terms adapts to the age (`l_max ≈ √(16/t)`, capped at 110).

Total heat is conserved: everything relaxes to the uniform temperature `(#sources)/(4π)`.

## Controls

- **Click**: add a heat source. **Drag**: rotate. **Scroll**: zoom.
- **Speed**: log-scale simulation speed. **Auto-scale colors**: normalize to the current peak (otherwise a fixed scale is used).
- **Pause / Reset**, and a cap on the number of simultaneous sources.

## Run locally

It's a single static file using three.js from a CDN:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy on GitHub Pages

1. Create a repo and add `index.html` and `README.md`.
2. Repo → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Your simulation will be live at `https://<user>.github.io/<repo>/`.
