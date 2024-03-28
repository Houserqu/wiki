```js
export function rotateImg(srcBase64: string, degrees: number, callback: (data: string) => void) {
  const canvas = document.createElement("canvas");
  const ctx = canvas.getContext("2d");
  const image = new Image();
  image.crossOrigin = "anonymous";

  image.onload = function () {
    canvas.width = degrees % 180 === 0 ? image.width : image.height;
    canvas.height = degrees % 180 === 0 ? image.height : image.width;

    ctx.translate(canvas.width / 2, canvas.height / 2);
    ctx.rotate((degrees * Math.PI) / 180);
    ctx.drawImage(image, image.width / -2, image.height / -2);

    callback(canvas.toDataURL());
  };

  image.src = srcBase64;
}
```

将图片转成 base64，再通过 cancas 旋转，输出旋转后的 base64，便于静态化