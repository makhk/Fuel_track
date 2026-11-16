# Fuelwise — Fuel & Mileage Tracker

A responsive, static fuel log designed for GitHub Pages. It tracks multiple vehicles, fuel spend, litres, odometer readings, estimated mileage and calculated fill-to-fill mileage.

## Publish with GitHub Pages

1. Create a repository (for example, `fuel-mileage-tracker`).
2. Upload `index.html` and this `README.md` to the repository root.
3. In **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. Open the Pages URL GitHub provides.

## Store your JSON in your own repository

1. Create a private repository for your data (recommended; it can be the same repo).
2. Create a **fine-grained personal access token** restricted to that repository, with **Contents: Read and write** permission.
3. In Fuelwise, choose **Repository sync** and enter owner, repository, branch, file path and token.
4. The app reads/writes `fuel-log.json` using the GitHub Contents API. The token is held in page memory only (not written to local storage or the JSON export). Re-enter it after a page refresh.

Security note: a remembered token is stored unencrypted in browser local storage. Anyone with access to that browser profile, or malicious JavaScript running on the site, could potentially access it. Use a fine-grained token limited to this single private repository, on a trusted personal device; revoke it from GitHub if the device is lost or shared. For stronger security, replace browser-token access with a server-side proxy or GitHub App.

## Mileage calculation

For each vehicle, entries are ordered by odometer reading:

`actual km/L = (current odometer − previous odometer) ÷ litres added in current entry`

This is a fill-to-fill estimate and is most accurate when each entry is recorded after filling the tank to the same level. The first entry for a vehicle has no actual mileage yet; its mileage is calculated when the next entry is recorded.

## JSON import/export

Use **Export JSON** to download the complete log. **Import JSON** replaces the current browser data after confirmation. The file format is:

```json
{
  "version": 1,
  "entries": [
    {
      "id": "unique-id",
      "vehicle": "Honda City",
      "date": "2026-11-16",
      "odo": 45230,
      "amount": 1500,
      "litres": 12.5,
      "estimate": 18
    }
  ]
}
```

No build tools or dependencies are required.

## Appearance and charts

Use the header theme button to switch between light and dark themes; the choice is remembered on the device. The dashboard includes a mileage trend line (actual vs estimated km/L) and a fuel-spend chart for the selected vehicle, using up to the latest 12 fill-ups.
