DEMO=platformer
CC=gcc

INCS= -I ./include -I ../../include

CFLAGS= $(INCS) -std=gnu99 -Wall -Werror -Wno-unused -O3 -g
C_FILES= $(wildcard src/*.c)
OBJ_FILES= $(addprefix obj/,$(notdir $(C_FILES:.c=.o)))

PLATFORM = $(shell uname)

ifeq ($(findstring Linux,$(PLATFORM)),Linux)
	OUT=$(DEMO)
	LFLAGS=-L../../ -lcorange -lGL -lSDL2 -lSDL2_net -lSDL2_mixer -lm
endif

ifeq ($(findstring Darwin,$(PLATFORM)),Darwin)
	OUT=$(DEMO)
	LFLAGS=-L../../ -lcorange -framework OpenGL -lSDLmain -lSDL2
endif

ifeq ($(findstring MINGW,$(PLATFORM)),MINGW)
	OUT=$(DEMO).exe
	LFLAGS=-L../../ ../../corange.res -lcorange -lmingw32 -lSDL2main -lSDL2 -lSDL2_Mixer -lSDL2_Net -lopengl32
endif

$(OUT): $(OBJ_FILES)
	$(CC) -g $(OBJ_FILES) $(LFLAGS) -o $@

obj/%.o: src/%.c | obj
	$(CC) $< -c $(CFLAGS) -o $@

obj:
	mkdir obj
	
lib:
	mkdir lib
	
clean:
	rm $(OUT) $(OBJ_FILES)

