# LEARNING-JOURNAL

# Colin Cupid

## 10/02/2021

I am very relieved that there are no tutorials needed for this project although I think that I am confident enough to get them them done if I need to. 
I am already getting ideas about the components I want to do and the game poroject. 
I  saw a tutorial on a rotating cube game. This will more than likely be the direction I turn to.

## 12/0202021

I am not sure that I understand the Markdown language mark is suggesting we use, my dyslexia and dyspraxia is making it very difficult for me to grasp how it works. I will need a few weeks of using it everyday for it to sink in. there are too many variables that can be used. That maybe an over statement but to me it feels that week. it has knocked my confidence a bit but I will try.

## 16/02/2021

Figuring out what components I want to use has not been difficult. Figuring out how to make them work together has been  challenge because agaiun I do not fully understand the commands that you would use to connect components to work together. This is an area I would like to develop on. I have started watching YouTube videos on the subject and it is a slow process but I im enjoying the journey so its not to bad. 

## 23/03/2021

'*How to program*' by Brackeys has beena good video. I tend to go back to it to refresh my memory about the subject. Brackeys in General has been a great resource as well games by James. Being able to have the compenents explained to you is great. Paul also does a great job of this but Iit awlays makes me want to understand it more. I have found thathe easiest way to learn is to complete tutorials on YouTube or get a 1-1 session with Paul. 

## 24/03/2021

I think have got mey head around Markdown language. I will spend some time going over it again to make sure.

## 26/03/2021

I have spotted an error in the grades for semester one work and notified Paul.

## 01/04/2021

I have been playing around with compnents and have surprised my self at how little erros I have found. I tried top find the simplest scripts possble so that they are not over complicated and difficult to understand. I am not sure if I will be explaining them corectly but I am very cofident that they work. Work together is another story. How do i get the 5 indivudla compnents to work together??


## 19/04/2021

a tutorial I was completeing is not working, So I asked paul for help. I was for a rotating cube mechanism. It needs work but once completed will show a good demo of the movement for my AGP game. Its the anniversary of my friends Murder today, I am not feeling great :(


## 27/04/2021

Paul has been going over some student request but I have not been able to focus because my friend was murdered this time last year. Her murderer was finally sentenced and it has made me sad and very distracted. I will request a break from studeis. But I wanted to go over my AGP demo with him before i did this.

{
    Vector2 firstPressPos;
    Vector2 secondPressPos;
    Vector2 currentSwipe;
    Vector3 previousMousePosition;
    Vector3 mouseDelta;
    //Int cubeStatus = 0; //when cube is idle.

    public GameObject target;
    float speed = 200f;

    // Start is called before the first frame update
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {
       Swipe();
       Drag();

    }

    void Drag()
    {
        if (Input.GetMouseButton(1))
        {
            // while the mouse button is held down the cube can be moved around its central axis to provide visual feedback
            mouseDelta = Input.mousePosition - previousMousePosition;
            mouseDelta *= 0.1f; // reduction of rotation speed
            transform.rotation = Quaternion.Euler(mouseDelta.y, -mouseDelta.x, 0) * transform.rotation;
        }
        else
        {
            // automatically move to the target positition
               if (transform.rotation != target.transform.rotation)
               {
                var step = speed * Time.deltaTime;
                transform.rotation = Quaternion.RotateTowards(transform.rotation, target.transform.rotation, step);
               }
        }
        previousMousePosition = Input.mousePosition;


    }
[12:31]
void Swipe()
    {
         if (Input.GetMouseButtonDown(1))
        {
            // get the 2D position of the First mouse Click
            firstPressPos = new Vector2(Input.mousePosition.x, Input.mousePosition.y);

        }
        if (Input.GetMouseButtonUp(1))
        {
        //get the 2nd position of the second mouse click
        secondPressPos = new Vector2(Input.mousePosition.x, Input.mousePosition.y);
        //create a vector from the first and second click postions
        currentSwipe = new Vector2(secondPressPos.x - firstPressPos.x, secondPressPos.y - firstPressPos.y);
        //normalize the 2D vector
        currentSwipe.Normalize();


        if (LeftSwipe(currentSwipe))
        {
        target.transform.Rotate(0, 90, 0, Space.World);
        }
        else if (RightSwipe(currentSwipe))
        {
        target.transform.Rotate(0, -90, 0, Space.World);
        }
        else if (UpLeftSwipe(currentSwipe))
        {
            target.transform.Rotate(90, 0, 0, Space.World);
        }
        else if (UpRightSwipe(currentSwipe))
        {
            target.transform.Rotate(0, 0, -90, Space.World);
        }
        else if (DownLeftSwipe(currentSwipe))
        {
            target.transform.Rotate(0, 0, 90, Space.World);
        }
        else if (DownRightSwipe(currentSwipe))

        {
            target.transform.Rotate(-90, 0, 0, Space.World);
        }
        }
[12:31]
}
    bool LeftSwipe(Vector2 swipe)
    {
        return currentSwipe.x < 0 && currentSwipe.y > -0.5f && currentSwipe.y < 0.5f;
    }

    bool RightSwipe(Vector2 swipe)
    {
        return currentSwipe.x > 0 && currentSwipe.y > -0.5f && currentSwipe.y < 0.5f;
    }

    bool UpLeftSwipe(Vector2 swipe)
    {
        return currentSwipe.y > 0 && currentSwipe.x <0f;
    }

    bool UpRightSwipe(Vector2 swipe)
    {
        return currentSwipe.y > 0 && currentSwipe.x > 0f;
    }

    bool DownLeftSwipe(Vector2 swipe)
    {
        return currentSwipe.y < 0 && currentSwipe.x < 0f;
    }

    bool DownRightSwipe(Vector2 swipe)
    {
        return currentSwipe.y < 0 && currentSwipe.x > 0f;
    }
}

 No idea whats wrong with this code.
 
 ## 30/04/2021
 
My computer is playing up, I have had to switch to using a different computer and found out that the installation on the new computer is not the same as the Unity we use at university and cant be changed because its belongs to some who his working on a project that uses the build already sinstalled. I feel like the project part of the Programming course work is already complete but, I cant check the project files due to the incompatible build. I have decided to go for something I have never done before, I gong to make a game with a weapon, probably a gun.

## 02/05/2021

public class WeaponController : MonoBehaviour
{
    public GameObject projectile;
    public Transform spawnPoint;
    public float recoilForce;

    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody(>);
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            var p = transform.position;
            Instantiate(projectile, spawnPoint.position, transform.rotation):

            if (recoilForce > 0)
                rb.AddForce(-transform.forward * recoilForce, ForceMode.Impulse);
        }
    }
///
I cant get the above script to work at all. grrrrrrrrr!!


## 05/05/2021

after a few days I came back to thi sand figured it out. (very hard to do with DS.
public class WeaponController : MonoBehaviour
{
    public GameObject projectile;
    public Transform spawnPoint;
    public float recoilForce;

    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            var p = transform.position;
            Instantiate(projectile, spawnPoint.position, transform.rotation);

            if (recoilForce > 0)
                rb.AddForce(-transform.forward * recoilForce, ForceMode.Impulse);
        }
    }
I couple of things were just in the wrong place. Using the techniques from last sememster, finding errors is getting easier for me.

## 06/05/2021

**This script is broken**

{
    public float speed;
    private Renderer r;
    private Rigidbody rb.;
    
    private void Start()
    {
        r = GetComponent<Renderer>();
        rb = GetComponent<Rigidbody>();
        rb.velocity = transform.forward * speed;
    }

    private void Update()
    {
        if (r.isViisble)
            return;
        
        Destroy(gameObject);
    }
    
    ///
    
    
    ## 01/06/2021
    
    This script is broken {
    public float speed;
    private Renderer r;
    private Rigidbody rb.;
    
    private void Start()
    {
        r = GetComponent<Renderer>();
        rb = GetComponent<Rigidbody>();
        rb.velocity = transform.forward * speed;
    }

    private void Update()
    {
        if (r.isViisble)
            return;
        
        Destroy(gameObject);
    }

/// 

fixed :)









