Testable BlogCreateAction

```php
<?php

class BlogCreateAction extends Action
{
    public function action()
    {
        // is this a POST request?
        if ($this->request->isPost()) {

            // yes, retain incoming data
            $data = $this->request->getPost('blog');

            // create a blog post instance
            $blog = $this->blog_model->newInstance($data);

            // is the new instance valid?
            if ($blog->isValid()) {
                $blog->save();
            }

        } else {
            // not a POST request, use default values
            $blog = $this->blog_model->getDefault();
        }

        // return action data for responder
        return array('blog' => $blog);
    }

    public function __invoke()
    {
        $actionData = $this->action();
        $this->responder->setData($actionData);
        $this->responder->__invoke();
    }
}
?>
