# sobel_img

let img;
let sobelImage;
let scharrImage;

function preload() {
  img = loadImage('https://cdn.mkhealth.co.kr/news/photo/202107/53894_55528_5330.jpg');
}

function setup() {
  createCanvas(img.width * 2, img.height);
  
  // 원본 이미지 표시
  image(img, 0, 0);
  
  // Sobel 연산을 적용한 이미지 생성
  sobelImage = createImage(img.width, img.height);
  sobelImage.loadPixels();
  img.loadPixels();
  for (let x = 1; x < img.width - 1; x++) {
    for (let y = 1; y < img.height - 1; y++) {
      let c00 = color(img.get(x - 1, y - 1));
      let c01 = color(img.get(x, y - 1));
      let c02 = color(img.get(x + 1, y - 1));
      let c10 = color(img.get(x - 1, y));
      let c12 = color(img.get(x + 1, y));
      let c20 = color(img.get(x - 1, y + 1));
      let c21 = color(img.get(x, y + 1));
      let c22 = color(img.get(x + 1, y + 1));

      let gx = -c00.levels[0] - 2 * c10.levels[0] - c20.levels[0] + c02.levels[0] + 2 * c12.levels[0] + c22.levels[0];
      let gy = -c00.levels[0] - 2 * c01.levels[0] - c02.levels[0] + c20.levels[0] + 2 * c21.levels[0] + c22.levels[0];
      
      let magnitude = sqrt(gx * gx + gy * gy);
      sobelImage.set(x, y, color(magnitude));
    }
  }
  sobelImage.updatePixels();
  image(sobelImage, img.width, 0);
  
  // Scharr 연산을 적용한 이미지 생성
  scharrImage = createImage(img.width, img.height);
  scharrImage.loadPixels();
  img.loadPixels();
  for (let x = 1; x < img.width - 1; x++) {
    for (let y = 1; y < img.height - 1; y++) {
      let c00 = color(img.get(x - 1, y - 1));
      let c01 = color(img.get(x, y - 1));
      let c02 = color(img.get(x + 1, y - 1));
      let c10 = color(img.get(x - 1, y));
      let c12 = color(img.get(x + 1, y));
      let c20 = color(img.get(x - 1, y + 1));
      let c21 = color(img.get(x, y + 1));
      let c22 = color(img.get(x + 1, y + 1));

      let gx = -3 * c00.levels[0] - 10 * c10.levels[0] - 3 * c20.levels[0] + 3 * c02.levels[0] + 10 * c12.levels[0] + 3 * c22.levels[0];
      let gy = -3 * c00.levels[0] - 10 * c01.levels[0] - 3 * c02.levels[0] + 3 * c20.levels[0] + 10 * c21.levels[0] + 3 * c22.levels[0];
      
      let magnitude = sqrt(gx * gx + gy * gy);
      scharrImage.set(x, y, color(magnitude));
    }
  }
  scharrImage.updatePixels();
  image(scharrImage, img.width * 2, 0);
}
