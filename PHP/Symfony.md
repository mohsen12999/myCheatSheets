# Symfony

## Requirements & Install

* php > 7.1
* install composer
* install [Symfony](https://symfony.com/download)
  * If you are building a traditional web application: `symfony new --full my_project`
  * If you are building a microservice, console application or API: `symfony new my_project`
* without install and make project with composer
  * traditional web application: `composer create-project symfony/website-skeleton my_project_name`
  * microservice, console application or API: `composer create-project symfony/skeleton my_project_name`
* Running: `symfony server:start`
* Installing Packages: `composer require logger`
* Checking Security Vulnerabilities: `symfony check:security`
* Demo application: `symfony new --demo my_project_name`

## get env in linux

* install lamp stack [eg. bitnami lampstack]
* `chmod +x [file name.run]`
* `./[file name.run]`
* check only simphony and phpmyadmin and uncheck others and install
* open program -> [go to application]
* `home/lampstack/apache/htdocs`
* install php7.2 php7.2-cli php7.2-common php7.2-musql php7.2-json ....
* install composer

## install Symfony

* install all thing for making website: `composer create-project symfony/website-skeleton my_project_name`
* install only minimum requirement: `composer create-project symfony/skeleton my_project_name`
* see bundle in flex.symfony.com

## make controller

* need to install `make-bundle` -> `composer require make`
* need to install `annotations` -> `composer require annotations`
* `php bin/console make:controller MainController`
* can use annotaions /*@Route... or config/routs.yaml for routing

* can see page in 'localhost:8080/project-name/public/index.php/main'
* can use `php bin/console server:start` to run in simple address -> `composer require server`

### change controller

```php
// use Symfony\Component\HttpFoundation\Response;
return new Response('<h1>Welcome!</h1>')
```

### input to controller

```php
// use Symfony\Component\HttpFoundation\Response;
// use Symfony\Component\HttpFoundation\Request;
/* @Route("/custom/{name?}","custom") */
public function custom(Request $request)
{
  $name = $request->get('name');
  return new Response('<h1>Welcome '.$name.'!</h1>')
}
```

* `{name}` is required, `{name?}` is optional
* for see request info -> use `dump` -> `composer require dump`

# make view

* use twig -> `composer require template`

### simpla view

```php
// in controller
return $this->render('home/index.html.twig'); // serch for template in 'template/home/index.html.twig'
```

### send param to view

```php
// in controller
return $this->render('home/custom.html.twig',['name'=>$name]);
```

```twig
// in twig template
<h1> welcome {{ name }} </h1>
```

### use layout

```twig
{% extends('base.html.twig') %}
{% block body %}
  <h1> welcome {{ name }} </h1>
{% endblock %}
```

### generate url

* use name for route

```twig
<a href="{{ path('home') }}" > go to home </a>
<a href="{{ path('home', {name: "mohsen"}) }}" > go to home </a>
```

## create database

* install `orm-pack` -> `composer require doctrine`
* change .env file for connection
* make db from console -> `php bin/console doctrine:database:create`
* problem in connection -> go to phpmyadmin -> `mysql` db -> `sql` tab -> 'GRANT ALL PRIVILEGES ON *.* TO root@127.0.0.1 IDENTIFIED BY `000000` WITH GRANT OPTION'

## make table

* `php bin/console make:entity` -> ask for name and field
* firt migration ->`php bin/console doctrine:schema:create`
* later migration ->`php bin/console doctrine:schema:update --dump-sql` -> only see query
* later migration ->`php bin/console doctrine:schema:update --force` -> run query

## route prefix

* `/* @Route('/post','post.') */` before controller class, make prefix for all function in it
* see all route -> `php bin/console debug:router`

## create entity

```php
// controller
// use App\Entity\Post;
  $post = new Post();
  $post->setTitle('this is going to be a title');
  // entity manager
  $em = $this->getDoctrine()->getManager();
  em->persist($post);
  em->flush();
```

## read from database

```php
// controller
// use App\Repository\PostRepository;
public function index(PostRepository $postRepository) // dependency injection
{
  $posts = $postRepository->findAll()
}
```

* findAll -> return array of all row
* findBy -> return array by something
* find -> by pk return one or null
* findOneBy -> return one or null by somthing

```twig
// twig file
<ul>
  {% for post in posts %}
    <li>{{ post.title }}</li>
  {% endfor %}
</ul>
```

* add link

```twig
<ul>
  {% for post in posts %}
    <li><a href="{{ path('post.show',{id: post.id}) }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```

```php
// controller
/* @Route("/show/{id}",name="show") */
public function show($id, PostRepository $postRepository)
{
  $post = $postRepository->find($id);
  dump($post);
}

// or use

/* @Route("/show/{id}",name="show") */
public function show(Post $post)
{
  dump($post);
}
```

## remove from database

```php
/* @Route("/delete/{id}",name="delete") */
public function show(Post $post)
{
  $em = $this->getDoctrine()->getManager();
  $em->persist($post);
  $em->flush();
  
  // redirect
  return $this->redirect($this->generateUrl('post.index'));
}
```

## flase message

```php
// in controller
// add flah message
$this->addflash('success','Post was Removed')
```

```twig
// in twig file
{% for message in app.flashes('success') %}
  <div class="alert alert-success">
    {{ message }}
  </div>
{% endfor %}
```

## make form

* `php require form validator`
* `php bin/console make:form` -> choose name & entity

```php
// in controller
public function create(Request $request)
{
  $post = new Post();
  $myform = $this->createForm(FormName::class, $post);
  $myform->handleRequest($request);
  if($myform->isSubmitted())
  {
    $em=$this->getDoctrine()->getManager();
    $em->presist($post);
    $em->flush();
    return $this->redirect($this->generateUrl('post.index'));
  }
  return $this->render('post/create.html.twig',['theform' => $myform->createView()])
}
```

```twig
{{ form(theform) }}
```

* add submit to builder class

```twig
// src/form/FormName -> buildForm
// use Symfony\Component\Form\Extention\Core\Type\SubmitType;
  ->add('save', SubmitType::class,[
     'atrr' => [ 'class' => 'btn btn-primary float-right' ]
  ])
```

* form theme -> config/package/twig.yaml ->add `form_theme:'bootstrap_4_layout.html.twig'`

* `composer require profiler` to see what happen as toolbar in page
* add validator to entity and use `if($form->isValid())` or `$form.getError()` 

## Authenticate

* `composer require security`
* `php bin/console make:user` -> `php bin/console doctrine:schema:update --force`
* `php bin/console make:auth`

```php
// make user
public function register(Request $request, UserPasswordEncoderInterface $passwordEncoder)
{
  $form = $this->createFormBuilder()
    ->add('username')
    ->add('password',RepeatedType::class,[
     'type' => PasswordType::class,
     'required' =>true
    ])
    ->add('register', SubmitType::class,['attr'=>['class'=>'btn btn-success float-right']])
    ->getForm();

  $form->handleRequest($request);
  if($form->isSubmited())
  {
    $data=$form->getData();
    $user=new User();
    $user->setUsername($data['username']);
    $user->setPassword($passwordEncoder->($user,$data['password']));
    em->persist($user);
    em->flush();
    // redirect to login page
  }
  // go to register page
}
```

### logout

* in config ->`security.yaml`-> `firewalls:` -> `main` ->add  `logout: path: app_logout`
* in `SecurityController.php` add function 'logout' sith rout 'app_logout'
* in config ->`security.yaml`->`access_control`-> add `- {path: ^/login, roles: IS_AUTHENTICATED_ANONYMOUSLY}`

```twig
{% if is_granted('IS_AUTHENTICATED_FULLY') %}
  <a href="{{ path('app_logout') }}">logout</a>
{% endif %}
```

## change entity

* add var to Entity

```php
// Post.php
/* @ORM\Column("string",length=100)
private $image;
```

* for add method -> `php bin/console make:entity --regenerate` -> press enter to check all -> make methos in entity for us
* migrate `php bin/console doctrine:schema:update --force`

```php
// in src/form -> `buildForm` function
  ->add('attachment',FileType:class,[
    'mapped' => false // if entity not have this field
  ])
```

* in config/services.yaml -> in `parameters` add -> `upload_dir: '%kernel.project_dir%/public/uploads/'`

```php
// in controller
  $file = $request->files->get('post')['attachment'];
  if($file)
  {
    $filename = md5(unigid()).'.'.$file->guessClientExtention(); // random filename
    $file.move($this.getParameter('uploads_dir'),$filename);
    $post->setImage($filename);
  }
```

## make relationship

```php
// in Post entity
/* @ORM\ManyToOne(targetEntity="App\Entity\Category", inversedBy="post") */
private $category;
```

```php
// in Category entity
/* @ORM\OneToMany(targetEntity="App\Entity\Post", mappedBy="category") */
private $post;
```

* make migration and update db

```php
// in src\form -> buildForm
   ->add('category',EntityType::class,[ 'class'=>Category::class ]) // need to implement string function in Category entity
```

```php
// in Category entity
public function __toString()
{
  return $this->name;
}
```

## make custome query function

```php
// in src/repository/PostRepositiry.php
public function findPostWithCategory(inr $id)
{
  $qb = $this->createQueryBuilder('p');
  $qb->select('p.title')->where('p.id =: id')->setParameter('id', $id);
  return $qb->getQuery()->getResult();
}
```

```php
// in controller
$post = $postRepository->findPostWithCategory($id);
```

* for more info

```php
// in src/repository/PostRepositiry.php
public function findPostWithCategory(inr $id)
{
  $qb = $this->createQueryBuilder('p');
  $qb->select('p.title')
    ->addSelect('p.id AS post_id')
    ->addSelect('c.name')
    ->addSelect('c.id As cat_id')
    ->innerJoin('p.category','c')
    ->where('p.id =: id')
    ->setParameter('id', $id);
  return $qb->getQuery()->getResult();
}
```

## Services

* services live in container

```php
// in src/services add file FileUploader.php
<?php 
namespace App\Services;
class FileUploader {
  public function __construct(ContainerInterface $container)
  {
     $this.container = $container;
  }
  public function uploadFile(UploadedFile $file)
  {
     // ...
  }
}
```

```php
// in controller
public function Create(Request $request, FileUploader $fileUploader)
{
  // ...
}
```