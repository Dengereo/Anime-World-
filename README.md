# Anime-World-
Dengereo 
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 10f;
    private Rigidbody2D rb;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        MovePlayer();
    }

    void MovePlayer()
    {
        float move = Input.GetAxis("Horizontal");
        rb.velocity = new Vector2(move * moveSpeed, rb.velocity.y);

        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
        }
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
        }
    }

    private void OnCollisionExit2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = false;
        }
    }
}
using UnityEngine;

public class UIController : MonoBehaviour
{
    public PlayerController player;
    private bool isRunning = false;

    public void OnMoveLeft()
    {
        player.rb.velocity = new Vector2(-player.moveSpeed, player.rb.velocity.y);
    }

    public void OnMoveRight()
    {
        player.rb.velocity = new Vector2(player.moveSpeed, player.rb.velocity.y);
    }

    public void OnJump()
    {
        if (player.isGrounded)
        {
            player.rb.velocity = new Vector2(player.rb.velocity.x, player.jumpForce);
        }
    }

    public void ToggleRun()
    {
        isRunning = !isRunning;
        player.moveSpeed = isRunning ? player.moveSpeed * 2 : player.moveSpeed / 2;
    }
}
