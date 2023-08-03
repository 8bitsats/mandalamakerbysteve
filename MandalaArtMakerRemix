// By Steve's Makerspace
// Video about it here: https://youtu.be/R3vZSu6gyog

let strokeW = 2; // how thick the lines are - try putting to 5
let overlap,
  beziers,
  sym,
  layers,
  alph,
  strokeYN,
  ang,
  a1x,
  a1y,
  a2x,
  a2y,
  x1,
  x2,
  y1,
  y2,
  hSize,
  cush,
  petalSlider,
  layersSlider,
  alphaSlider,
  randomPetalButton,
  randomLayersButton,
  randomAlphaButton,
  outlineButton,
  noOutlineButton,
  randOutButton,
  curve1Button,
  curve2Button,
  randCurveButton,
  overlapButton,
  noOverlapButton,
  randOverlapButton,
  newArtButton,
  printButton;
let pRand = -1;
let lRand = -1;
let aRand = -1;
let cRand = true;
let randOverl = true;

function setup() {
  let size = min(windowWidth, windowHeight) - 110;
  canvas = createCanvas(size, size);
  canvas.position(10, 95);
  hSize = size / 2;
  angleMode(DEGREES);
  translate(width / 2, height / 2);

  // create user interface
  let noPetals = createElement("noPetals", "# of petals");
  noPetals.position(40, 0);
  petalSlider = createSlider(8, 30, 17);
  petalSlider.position(10, 20);
  let noLayers = createElement("noLayers", "# of layers");
  noLayers.position(175, 0);
  layersSlider = createSlider(3, 30, 17);
  layersSlider.position(150, 20);
  let alpha = createElement("alpha", "alpha");
  alpha.position(330, 0);
  alphaSlider = createSlider(25, 100, 50);
  alphaSlider.position(290, 20);

  randomPetalsButton = createButton("random");
  randomPetalsButton.position(40, 45);
  randomPetalsButton.style("background-color", "lightgreen");
  randomPetalsButton.mousePressed(petalsRandom);
  randomLayersButton = createButton("random");
  randomLayersButton.position(180, 45);
  randomLayersButton.style("background-color", "lightgreen");
  randomLayersButton.mousePressed(layersRandom);
  randomAlphaButton = createButton("random");
  randomAlphaButton.position(320, 45);
  randomAlphaButton.style("background-color", "lightgreen");
  randomAlphaButton.mousePressed(alphaRandom);

  newArtButton = createButton("new art");
  newArtButton.position(110, 70);
  newArtButton.style("background-color", "yellow");
  newArtButton.mousePressed(newArt);
  printButton = createButton("save jpg");
  printButton.position(250, 70);
  printButton.style("background-color", "yellow");
  printButton.mousePressed(saveJpg);

  outlineButton = createButton("outline");
  outlineButton.position(430, 0);
  outlineButton.mousePressed(outline);
  noOutlineButton = createButton("no outline");
  noOutlineButton.position(500, 0);
  noOutlineButton.mousePressed(noOutline);
  randOutButton = createButton("random");
  randOutButton.position(580, 0);
  randOutButton.mousePressed(randOutline);
  randOutline();

  curve1Button = createButton("style 1");
  curve1Button.position(430, 30);
  curve1Button.mousePressed(curve1);
  curve2Button = createButton("style 2");
  curve2Button.position(505, 30);
  curve2Button.mousePressed(curve2);
  randCurveButton = createButton("random");
  randCurveButton.position(580, 30);
  randCurveButton.mousePressed(randCurve);
  randCurve();

  overlapButton = createButton("> overlap");
  overlapButton.position(430, 60);
  overlapButton.mousePressed(overlapYes);
  noOverlapButton = createButton("< overlap");
  noOverlapButton.position(505, 60);
  noOverlapButton.mousePressed(noOverlap);
  randOverlapButton = createButton("random");
  randOverlapButton.position(580, 60);
  randOverlapButton.mousePressed(randOverlap);
  randOverlap();

  colorMode(HSB, 256, 100, 100, 100);
  newArt();
}

function newArt() {
  background(0);
  // get variable values
  if (pRand == 1) {
    sym = petalSlider.value();
  } else {
    sym = random(8, 30);
  }
  ang = 360 / sym;
  if (lRand == 1) {
    layers = layersSlider.value();
  } else {
    layers = random(3, 30);
  }
  cush = (hSize / layers) * 0.9; // cushion between each layer
  if (aRand == 1) {
    alph = alphaSlider.value();
  } else {
    alph = random(25, 100);
  }
  if (strokeRand == 1) {
    strokeYN = round(random(1));
  }
  if (cRand == true) {
    beziers = round(random(1));
  }
  if (randOverl == true) {
    overlap = round(random(1));
  }
  let outlineNote
  if (strokeYN==1){outlineNote="yes"}
  else {outlineNote = "no"}
  let overlapNote
  if (overlap == 0){ overlapNote="less"}
  else {overlapNote="more"}
  print('petals:',round(sym,1), '; layers:',round(layers,1),';alpha:',round(alph),';outline:',outlineNote,';style:',beziers+1,';overlap:',overlapNote)

  // calculate points for each layer, starting with outside pedals and going inward
  for (let j = 0; j < layers; j++) {
    x1 = random(hSize * 0.75 - j * cush, hSize * 0.85 - j * cush);
    y1 = 0;
    x2 = random(hSize * 0.9 - j * cush, hSize - j * cush);
    y2 = 0;
    a1x = random(x1 * 1.2, x2 * 0.4);
    a2x = random(x2 * 0.5, x2 * 0.9);

    if (overlap == 0) {
      a1y = a1x * tan(ang);
      let maxa2y = a2x * tan(ang);
      a2y = random(20 / j, maxa2y);
    } else {
      a1y = random(20 / j, 100 - j * cush);
      if(a1y<1){a1y=a1x*tan(ang)}
      a2y = random(20 / j, 150 - j * cush);
      if(a2y<1){a2y=random(20/j,a2x*tan(ang))}
    }
    let hue = random(256);
    let sat = random(70, 100); //You could play
    let brt = random(75, 100); //with these too.
    fill(hue, sat, brt, alph);

    // draw one set of petals
    for (let i = 0; i < sym / 2; i++) {
      if (strokeYN == 1) {
        stroke(0);
        strokeWeight(strokeW);
      } else {
        noStroke();
      }
      if (beziers == 0) {
        beginShape();
        curveVertex(x1, 0);
        curveVertex(x1, 0);
        curveVertex(a1x, a1y);
        curveVertex(a2x, a2y);
        curveVertex(x2, 0);
        curveVertex(x2, 0);
        endShape();

        beginShape();
        curveVertex(x1, 0);
        curveVertex(x1, 0);
        curveVertex(a1x, -a1y);
        curveVertex(a2x, -a2y);
        curveVertex(x2, 0);
        curveVertex(x2, 0);
        endShape();
        if (strokeYN == 1) {
          stroke(hue, sat, brt, alph);
          line(x1, 0, x2, 0);
        }
      } else {
        bezier(x1, y1, a1x, a1y, a2x, a2y, x2, y2);
        bezier(x1, y1, a1x, -a1y, a2x, -a2y, x2, y2);
      }
      rotate(ang * 2);
    }rotate(ang);
  }
}

// Button functions
function petalsRandom() {
  pRand = pRand * -1;
  if (pRand == 1) {
    randomPetalsButton.style("background-color", "pink");
  } else {
    randomPetalsButton.style("background-color", "lightgreen");
  }
}
function layersRandom() {
  lRand = lRand * -1;
  if (lRand == 1) {
    randomLayersButton.style("background-color", "pink");
  } else {
    randomLayersButton.style("background-color", "lightgreen");
  }
}
function alphaRandom() {
  aRand = aRand * -1;
  if (aRand == 1) {
    randomAlphaButton.style("background-color", "pink");
  } else {
    randomAlphaButton.style("background-color", "lightgreen");
  }
}
function outline() {
  strokeYN = 1;
  strokeRand = 0;
  noOutlineButton.style("background-color", "pink");
  outlineButton.style("background-color", "lightgreen");
  randOutButton.style("background-color", "pink");
}
function noOutline() {
  strokeYN = 0;
  strokeRand = 0;
  noOutlineButton.style("background-color", "lightgreen");
  outlineButton.style("background-color", "pink");
  randOutButton.style("background-color", "pink");
}
function randOutline() {
  strokeRand = 1;
  noOutlineButton.style("background-color", "pink");
  outlineButton.style("background-color", "pink");
  randOutButton.style("background-color", "lightgreen");
}
function curve1() {
  beziers = 0;
  cRand = false;
  curve2Button.style("background-color", "pink");
  randCurveButton.style("background-color", "pink");
  curve1Button.style("background-color", "lightgreen");
}
function curve2() {
  beziers = 1;
  cRand = false;
  curve1Button.style("background-color", "pink");
  randCurveButton.style("background-color", "pink");
  curve2Button.style("background-color", "lightgreen");
}
function randCurve() {
  cRand = true;
  curve1Button.style("background-color", "pink");
  curve2Button.style("background-color", "pink");
  randCurveButton.style("background-color", "lightgreen");
}

function overlapYes() {
  overlap = 1;
  randOverl = false;
  overlapButton.style("background-color", "lightgreen");
  noOverlapButton.style("background-color", "pink");
  randOverlapButton.style("background-color", "pink");
}
function noOverlap() {
  overlap = 0;
  randOverl = false;
  overlapButton.style("background-color", "pink");
  noOverlapButton.style("background-color", "lightgreen");
  randOverlapButton.style("background-color", "pink");
}
function randOverlap() {
  randOverl = true;
  overlapButton.style("background-color", "pink");
  noOverlapButton.style("background-color", "pink");
  randOverlapButton.style("background-color", "lightgreen");
}

function saveJpg() {
  save("myCanvas.jpg");
}
