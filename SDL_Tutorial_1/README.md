README.md
===

## SDL2시작 빌드해 보기

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
#include <iostream>
#include <SDL.h>

int main(int, char**){
	if (SDL_Init(SDL_INIT_VIDEO) != 0){
		std::cout << "SDL_Init Error: " << SDL_GetError() << std::endl;
		return 1;
	}
	SDL_Quit();
	return 0;
}
```

---

### 참고사항

* SDL2.dll파일을 실행파일과 함께 넣어야 함.

---

### 참고사이트

* [사이트](https://www.willusher.io/sdl2%20tutorials/2013/08/15/lesson-0-visual-studio)