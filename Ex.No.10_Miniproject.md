# Ex.No: 10  Implementation of 3D Coin Collector

### DATE: 02.09.2026                                                                          
### REGISTER NUMBER : 212223230028

### AIM: 
To develop a 3D Coin Collector game in Unity using C# and basic AI/game-development techniques.

### Algorithm:
1. Create a new 3D Unity project using the Built-in Render Pipeline.
2. Create the game environment with a ground plane and boundary walls.
3. Create a capsule as the player and add Rigidbody and Collider components.
4. Implement player movement using C# and keyboard input.
5. Create coin objects and assign materials and colliders.
6. Implement coin rotation and collision-based coin collection.
7. Create a GameManager to maintain the score and total number of collected coins.
8. Add a countdown timer and display the score and time using TextMeshPro UI.
9. Implement Win and Game Over panels.
10. Add a Restart button to reload the game scene.
11. Test player movement, coin collection, timer, winning, game-over, and restart functionality.

### Program:
GameManager
```
using UnityEngine;
using UnityEngine.SceneManagement;
using TMPro;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    [Header("UI")]
    public TMP_Text scoreText;
    public TMP_Text timerText;
    public GameObject winPanel;
    public GameObject gameOverPanel;

    [Header("Game Settings")]
    public int totalCoins = 8;
    public float gameTime = 60f;

    private int score = 0;
    private int coinsCollected = 0;
    private float timer;
    private bool gameEnded = false;

    void Awake()
    {
        instance = this;
    }

    void Start()
    {
        timer = gameTime;

        score = 0;
        coinsCollected = 0;
        gameEnded = false;

        if (winPanel != null)
            winPanel.SetActive(false);

        if (gameOverPanel != null)
            gameOverPanel.SetActive(false);

        UpdateScoreUI();
        UpdateTimerUI();
    }

    void Update()
    {
        if (gameEnded)
            return;

        timer -= Time.deltaTime;

        if (timer <= 0)
        {
            timer = 0;
            GameOver();
        }

        UpdateTimerUI();
    }

    public void CollectCoin()
    {
        if (gameEnded)
            return;

        coinsCollected++;
        score += 10;

        UpdateScoreUI();

        if (coinsCollected >= totalCoins)
        {
            WinGame();
        }
    }

    void UpdateScoreUI()
    {
        if (scoreText != null)
            scoreText.text = "Score: " + score;
    }

    void UpdateTimerUI()
    {
        if (timerText != null)
            timerText.text = "Time: " + Mathf.Ceil(timer).ToString();
    }

    void WinGame()
    {
        gameEnded = true;

        if (winPanel != null)
            winPanel.SetActive(true);
    }

    void GameOver()
    {
        gameEnded = true;

        if (gameOverPanel != null)
            gameOverPanel.SetActive(true);
    }

    public void RestartGame()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}
```
CamerFollow

```
using UnityEngine;

public class CameraFollow : MonoBehaviour
{
    public Transform player;
    public Vector3 offset = new Vector3(0f, 12f, -8f);

    void LateUpdate()
    {
        if (player != null)
        {
            transform.position = player.position + offset;
            transform.LookAt(player);
        }
    }
}
```
CoinCollector

```
using UnityEngine;

public class CoinCollector : MonoBehaviour
{
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            GameManager.instance.CollectCoin();
            Destroy(gameObject);
        }
    }
}
```
CoinRotation

```
using UnityEngine;

public class CoinRotation : MonoBehaviour
{
    public float rotationSpeed = 100f;

    void Update()
    {
        transform.Rotate(0f, rotationSpeed * Time.deltaTime, 0f);
    }
}
```
PlayerMovement

```
using UnityEngine;
using UnityEngine.InputSystem;

public class PlayerMovement : MonoBehaviour
{
    public float speed = 5f;

    private Rigidbody rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        if (Keyboard.current == null)
            return;

        float x = 0f;
        float z = 0f;

        // Left / Right
        if (Keyboard.current.aKey.isPressed)
            x = -1f;

        if (Keyboard.current.dKey.isPressed)
            x = 1f;

        // Forward / Backward
        if (Keyboard.current.wKey.isPressed)
            z = 1f;

        if (Keyboard.current.sKey.isPressed)
            z = -1f;

        Vector3 movement = new Vector3(x, 0f, z);

        // Prevent faster diagonal movement
        movement = Vector3.ClampMagnitude(movement, 1f);

        rb.MovePosition(
            rb.position + movement * speed * Time.fixedDeltaTime
        );
    }
}
```


### Output:

<img width="1920" height="1020" alt="Screenshot 2026-09-01 105921" src="https://github.com/user-attachments/assets/ed16b675-8101-4cce-acc6-d2ec25b4bc07" />

<img width="1920" height="1020" alt="Screenshot 2026-09-01 105937" src="https://github.com/user-attachments/assets/cb94f40c-a40c-4839-820f-6aa1be5b38e4" />

<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/d18c526d-84cc-471b-8f57-fb053a39a4d0" />


### Result:
Thus, a 3D Coin Collector game was successfully developed using Unity and C# programming. The game implements player movement, coin collection, score tracking, countdown timer, win/game-over conditions, camera following, and restart functionality.

Thus, the 3D Coin Collector game was successfully developed using Unity and adopted basic AI/game-development technology for interactive gameplay.
