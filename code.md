HEADER{
	PROJECT "Space Defender Web"
	AUTHOR FABRIZIO RADICA
	YEAR 2026
	VER 1.1
}
SYSTEM PROMPT
{
	You are a senior, experienced Three.js developer
	Do not comment on the code.
	Adhere strictly to the instructions in this document.
	Do not make things up or beat about the bush.
}
CREDITS
{
	TITLE "SPACE DEFENDER"
	AUTHOR "FABRIZIO RADICA"
	YEAR 2026
	NOTE "SVILUPPATO IN METALINGUAGGIO"
	SHOW_ON title_screen
}
ENGINE
{
    FRAMEWORK ThreeJS
    VERSION r180
    LANGUAGE JavaScript
    MODULE_SYSTEM ESModules
    BUNDLER Vite
    TARGET_PLATFORM
    {
        Desktop
        Mobile
        Web
    }
    OUTPUT WebGL
}
RENDERING
{
    RENDERER WebGLRenderer
    ANTIALIAS false
    ALPHA false
    SHADOWS false
    PIXEL_RATIO auto
    RESOLUTION
    {
        WIDTH 1280
        HEIGHT 720
    }
    CLEAR_COLOR black
}
SCENE
{
    CAMERA Orthographic
    CAMERA_SETTINGS
    {
        SIZE 10
        NEAR 0.1
        FAR 1000
        POSITION 0 0 10
    }
    BACKGROUND
    {
        COLOR black
    }
}
INPUT
{
    SYSTEM BrowserInput
    KEYBOARD
    {
        MOVE_LEFT ArrowLeft
        MOVE_RIGHT ArrowRight
        FIRE Space
    }
    GAMEPAD
    {
        ENABLED true
        MOVE LeftStickX
        FIRE SouthButton
    }
    TOUCH
    {
        ENABLED true
        AUTO_SHOW on_touch_device
        BUTTONS
        {
            LEFT true
            RIGHT true
            FIRE true
        }
    }
}
PLAYER PlayerShip
{
    OBJECT_TYPE Sprite
    POSITION
    {
        X 0
        Y -7
    }
    MOVEMENT
    {
        AXIS horizontal
        SPEED 8
        LIMIT_TO_SCREEN true
    }
    SHOOT
    {
        FIRE_RATE 0.25
        PROJECTILE BulletPlayer
    }
    COLLISION
    {
        TYPE AABB
    }
}
PROJECTILE BulletPlayer
{
    SPEED 15
    DIRECTION up
    AUTO_DESTROY outside_screen
    COLLISION
    {
        TARGET enemy
    }
}
PROJECTILE BulletEnemy
{
    SPEED 8
    DIRECTION down
    AUTO_DESTROY outside_screen
    COLLISION
    {
        TARGET player
    }
}
ENEMIES Invaders
{
    TYPE formation

    LAYOUT_LANDSCAPE
    {
        GRID
        {
            ROWS 5
            COLUMNS 11
            SPACING_X 1.2
            SPACING_Y 1
        }
        SPRITE_SCALE 0.9
        MOVEMENT
        {
            HORIZONTAL_SPEED 2
            CHANGE_DIRECTION_ON_BORDER true
            EDGE_MARGIN 0.3
            STEP_DOWN 0.5
            SPEED_INCREASE overtime
        }
        SHOOT
        {
            RANDOM true
            FIRE_RATE 1.5
        }
    }

    LAYOUT_PORTRAIT
    {
        GRID
        {
            ROWS 4
            COLUMNS 7
            SPACING_X 0.95
            SPACING_Y 0.85
        }
        SPRITE_SCALE 0.7
        MOVEMENT
        {
            HORIZONTAL_SPEED 2
            CHANGE_DIRECTION_ON_BORDER true
            EDGE_MARGIN 0.6
            STEP_DOWN 0.25
            SPEED_INCREASE overtime
        }
        SHOOT
        {
            RANDOM true
            FIRE_RATE 1.5
        }
    }
}
ORIENTATION_HANDLING
{
    DETECT_CHANGE true
    ON_CHANGE
    {
        RESPAWN_ENEMIES true
        CLEAR_BULLETS true
        PRESERVE_SCORE true
        PRESERVE_LIVES true
        PRESERVE_WAVE true
    }
}
COLLISION_SYSTEM
{
    TYPE simple2D
    METHOD bounding_box
}
VISUAL_STYLE
{
    RETRO true
    SPRITE_FILTER nearest
    POST_PROCESS
    {
        CRT false
        BLOOM false
    }
}
OPTIMIZATION
{
    OBJECT_POOLING true
    FRUSTUM_CULLING true
    STATIC_OBJECTS true
}
ARCHITECTURE
{
    ECS false
    STRUCTURE
    {
        main.js
        game.js
        player.js
        enemies.js
        bullets.js
        collision.js
        input.js
    }
}
GENERATE
{
    HTML
    CSS
    JAVASCRIPT
    GAME_LOOP
    INPUT_MANAGER
    COLLISION_SYSTEM
    OBJECT_POOLING
    ENEMY_MANAGER
    ORIENTATION_HANDLER
    TOUCH_CONTROLS
}
