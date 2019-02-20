README.md
===

## SDL2 비트맵 그리기

---

### 개발환경

* Windows 10 64bits
* Visual Studio 2017 64bits

---

### 구현

* 추가 포함 디렉터리 : $(ProjectDir)SDL2-2.0.9\include\
* 추가 라이브러리 디렉터리 : $(ProjectDir)SDL2-2.0.9\lib\x64\
* 추가 종속성 : SDL2.lib;SDL2main.lib

```c
// SDL_Tutorial_1Dlg.h
#include <SDL.h>
```

```c
//BOOL CSDLTutorial1Dlg::OnInitDialog()
if (SDL_Init(SDL_INIT_VIDEO) != 0) {
	AfxMessageBox(_T("init Error"));
}
```

```c
SDL_Window* win = SDL_CreateWindowFrom(this->GetSafeHwnd());
if (win == nullptr) {
	AfxMessageBox(_T("Window Error"));
	SDL_Quit();
}

SDL_Renderer *ren = SDL_CreateRenderer(win, -1, SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC);

if (ren == nullptr) {
	SDL_DestroyWindow(win);
	AfxMessageBox(_T("SDL_CreateRenderer Error"));
	SDL_Quit();
}

string imagePath = "hello.bmp";
SDL_Surface *bmp = SDL_LoadBMP(imagePath.c_str());
if (bmp == nullptr) {
	SDL_DestroyRenderer(ren);
	SDL_DestroyWindow(win);
	AfxMessageBox(_T("SDL_LoadBMP Error"));
	SDL_Quit();
}

SDL_Texture *tex = SDL_CreateTextureFromSurface(ren, bmp);
//We no longer need the surface
SDL_FreeSurface(bmp);
if (tex == nullptr) {
	SDL_DestroyRenderer(ren);
	SDL_DestroyWindow(win);
	AfxMessageBox(_T("SDL_CreateTextureFromSurface Error"));
	SDL_Quit();
}

for (int i = 0; i < 3; ++i) {
	//First clear the renderer
	SDL_RenderClear(ren);
	//Draw the texture
	SDL_RenderCopy(ren, tex, NULL, NULL);
	//Update the screen
	SDL_RenderPresent(ren);
	//Take a quick break after all that hard work
	SDL_Delay(1000);
}

//Clean up our objects and quit
SDL_DestroyTexture(tex);
SDL_DestroyRenderer(ren);
SDL_DestroyWindow(win);
SDL_Quit();
```

---

### 참고사항

* SDL2.dll파일을 실행파일과 함께 넣어야 함.

---

### 참고사이트

* [사이트](https://github.com/Twinklebear/TwinklebearDev-Lessons/blob/master/Lesson1/src/main.cpp)