<script>
	import MapScroller from './MapScroller.svelte';
  import { isPortrait } from '../modules/store.js';
  import { isMobile } from "../modules/utils.js";
  import { makeColors } from "../modules/color.js";

  export let dataPath;
  export let imagePath;
  export let scrollY;
  export let mapSectionData;
  export let mapId;

  // Setting map style JSON and fonts
  const mapStyleUrl = import.meta.env.PROD ? `${dataPath}/style.json` : `${dataPath}/styleDev.json`
	const fontRegular = "Lato Regular"
	const fontBold = "Lato Bold"

  const mapBounds = {
    nyc: [[ -74.082046, 40.841011], [ -73.882857, 40.657249]],
    nyc_chelsea: [[ -74.032046, 40.781011], [ -73.972857, 40.707249]],
    nyc_midtown: [[ -74.002046, 40.801011], [ -73.942857, 40.727249]],
    nyc_central_park: [[ -74.002046, 40.831011], [ -73.942857, 40.757249]],
    nyc_statue: [[ -74.072046, 40.721011], [ -74.012857, 40.667249]]
  };

  const mapIcons = []
	const mapAttribution = {}
  const mapLegends = []
	const mapLayerOrder = [
		'statue-image',
		'central-park-image',
		'midtown-image',
		'chelsea-image',
    'nyc-image'
  ]

	const nycImgCoords = [
		[-73.974032,40.841011],
		[-73.882857,40.801994],
		[-73.990871,40.657249],
		[-74.082046,40.696352],
	]

	const mapSources = [
		// NEIGHBORHOOD IMAGE
		{		
			filepath: `${imagePath}/nyc.jpg`,
			sourceId: "nyc",
			dataType: "image",
			coordinates: 	nycImgCoords,
			layers: [
				{
					mapLayerId: "nyc-image",
					layerType: "raster",
					paint: {
						default: {
				      "raster-opacity": 1,
				      "raster-opacity-transition": {"duration": 300,"delay": 0}
						},
						two: {
							"raster-opacity": 0.5,
						},
						three: {
							"raster-opacity": 0.5,
						},
						four: {
							"raster-opacity": 0.5,
						},
						five: {
							"raster-opacity": 0.5,
						},
						six: {
							"raster-opacity": 0.5,
						},
						seven: {
							"raster-opacity": 1
						}
					}
				}
			]
		},
		{		
			filepath: `${imagePath}/chelsea.png`,
			sourceId: "nyc",
			dataType: "image",
			coordinates: 	nycImgCoords,
			layers: [
				{
					mapLayerId: "chelsea-image",
					layerType: "raster",
					paint: {
						default: {
				      "raster-opacity": 0,
				      "raster-opacity-transition": {"duration": 300,"delay": 0}
						},
						two: {
							"raster-opacity": 1
						},
						three: {
							"raster-opacity": 1
						},
						four: {
							"raster-opacity": 0
						},
						seven: {
							"raster-opacity": 1
						}
					}
				}
			]
		},
		{		
			filepath: `${imagePath}/midtown.png`,
			sourceId: "nyc",
			dataType: "image",
			coordinates: 	nycImgCoords,
			layers: [
				{
					mapLayerId: "midtown-image",
					layerType: "raster",
					paint: {
						default: {
				      "raster-opacity": 0,
				      "raster-opacity-transition": {"duration": 300,"delay": 0}
						},
						four: {
							"raster-opacity": 1
						},
						five: {
							"raster-opacity": 0
						},
						seven: {
							"raster-opacity": 1
						}
					}
				}
			]
		},
		{		
			filepath: `${imagePath}/central-park.png`,
			sourceId: "nyc",
			dataType: "image",
			coordinates: 	nycImgCoords,
			layers: [
				{
					mapLayerId: "central-park-image",
					layerType: "raster",
					paint: {
						default: {
				      "raster-opacity": 0,
				      "raster-opacity-transition": {"duration": 300,"delay": 0}
						},
						five: {
							"raster-opacity": 1
						},
						six: {
							"raster-opacity": 0
						},
						seven: {
							"raster-opacity": 1
						}
					}
				}
			]
		},
		{		
			filepath: `${imagePath}/statue.png`,
			sourceId: "nyc",
			dataType: "image",
			coordinates: 	nycImgCoords,
			layers: [
				{
					mapLayerId: "statue-image",
					layerType: "raster",
					paint: {
						default: {
				      "raster-opacity": 0,
				      "raster-opacity-transition": {"duration": 300,"delay": 0}
						},
						six: {
							"raster-opacity": 1
						},
						seven: {
							"raster-opacity": 1
						}
					}
				}
			]
		}
	]

	const mapTooltips = {}
</script>

<MapScroller
	{scrollY}
	{mapId}
	{mapSectionData}

	{mapStyleUrl}
	{mapIcons}
	{mapBounds}
	{mapAttribution}
	{mapLegends}
	{mapLayerOrder}
	{mapSources}
	{mapTooltips}
/>

<style>
	:global(.central) {
		background: #a7ffb9;
		font-weight: bold;
		padding: 2px 5px;
	}
	:global(.chelsea) {
		background: #d5ffff;
		font-weight: bold;
		padding: 2px 5px;
	}
	:global(.midtown) {
		background: #ffd7ff;
		font-weight: bold;
		padding: 2px 5px;
	}
	:global(.statue) {
		background: #72ffcf;
		font-weight: bold;
		padding: 2px 5px;
	}	
</style>
