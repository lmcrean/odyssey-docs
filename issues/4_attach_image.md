I'm trying to implement attach images to my messagedetail in message app

So far here's what's working.

# 1. Post Request working as expected in production API

post request: https://odyssey-api-f3455553b29d.herokuapp.com/messages/29/send/

with form-data:

```json
{
    "content": "hi there",
    "image": "test_image.jpg"
}
```

returns:

```
{
    "id": 124,
    "sender": 25,
    "recipient": 29,
    "content": "hi there",
    "image": "https://res.cloudinary.com/dh5lpihx1/image/upload/v1724759563/oksprn7ze6hvps9fbore.jpg",
    "date": "27 Aug 2024",
    "time": "11:52",
    "read": false,
    "sender_profile_image": "https://res.cloudinary.com/dh5lpihx1/image/upload/v1/media/images/default_profile_dqcubz.jpg",
    "recipient_profile_image": "https://res.cloudinary.com/dh5lpihx1/image/upload/v1/media/images/default_profile_dqcubz.jpg",
    "is_sender": true,
    "last_message": "hi there",
    "last_message_time": "11:52"
}
```

It has been tested thoroughly on the backend with unit tests.

I am using Django-rest framework.

# 2. Attempting to implement in the front-end

The Following file was previously working for sending messages without images.

```jsx
// src/pages/messaging/MessageDetailSendForm.js

import React, { useState } from "react";
import { useParams } from "react-router-dom";
import { axiosRes } from "../../api/axiosDefaults";
import Button from "react-bootstrap/Button";
import Form from "react-bootstrap/Form";
import Alert from "react-bootstrap/Alert";
import Container from "react-bootstrap/Container";

function MessageDetailSendForm({ setMessages }) {
  const { id } = useParams();
  const [content, setContent] = useState("");
  const [errors, setErrors] = useState({});

  const handleChange = (event) => {
    setContent(event.target.value);
  };

  const handleSubmit = async (event) => {
    event.preventDefault();


    try {
      const { data } = await axiosRes.post(`/messages/${id}/send/`, {
        content: content,
      });


      setMessages((prevMessages) => ({
        ...prevMessages,
        results: [...prevMessages.results, data],
      }));
      setContent("");
    } catch (err) {
      console.error("Error sending message:", err);
      if (err.response?.status !== 401) {
        setErrors(err.response?.data);
      }
    }
  };

  return (
    <Container>
      <Form onSubmit={handleSubmit}>
        <Form.Group>
          <Form.Label>New Message</Form.Label>
          <Form.Control
            as="textarea"
            rows={3}
            value={content}
            onChange={handleChange}
          />
        </Form.Group>
        {errors?.content?.map((message, idx) => (
          <Alert variant="warning" key={idx}>
            {message}
          </Alert>
        ))}
        <Button variant="primary" type="submit">
          Send
        </Button>
      </Form>
    </Container>
  );
}

export default MessageDetailSendForm;
```

# 3. Working reference - PostCreateForm
It is also worth noting that this PostCreate component is still working as expected and makes a similar Post Req with or without attached image.

```jsx
// src/pages/posts/PostCreateForm.js

import React, { useRef, useState } from "react";

import Form from "react-bootstrap/Form";
import Button from "react-bootstrap/Button";
import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";
import Container from "react-bootstrap/Container";
import Alert from "react-bootstrap/Alert";
import Image from "react-bootstrap/Image";

import Asset from "../../components/Asset";

import Upload from "../../assets/upload.png";

import styles from "../../styles/modules/PostCreateEditForm.module.css";
import appStyles from "../../App.module.css";
import btnStyles from "../../styles/modules/Button.module.css";

import { useHistory } from "react-router";
import { axiosReq } from "../../api/axiosDefaults";
import { useRedirect } from "../../hooks/useRedirect";

function PostCreateForm() {
  useRedirect("loggedOut");
  const [errors, setErrors] = useState({});

  const [postData, setPostData] = useState({
    title: "",
    content: "",
    image: "",
  });
  const { title, content, image } = postData;

  const imageInput = useRef(null);
  const history = useHistory();

  const handleChange = (event) => {
    setPostData({
      ...postData,
      [event.target.name]: event.target.value,
    });
  };

  const handleChangeImage = (event) => {
    if (event.target.files.length) {
      URL.revokeObjectURL(image);
      setPostData({
        ...postData,
        image: URL.createObjectURL(event.target.files[0]),
      });
    }
  };

  const handleSubmit = async (event) => {
    event.preventDefault();
    const formData = new FormData();

    formData.append("title", title);
    formData.append("content", content);
    formData.append("image", imageInput.current.files[0]);

    try {
      const { data } = await axiosReq.post("/posts/", formData);
      history.push(`/posts/${data.id}`);
    } catch (err) {
      
      if (err.response?.status !== 401) {
        setErrors(err.response?.data);
      }
    }
  };

  const textFields = (
    <div className="text-center">
      <Form.Group>
        <Form.Label>Title</Form.Label>
        <Form.Control
          type="text"
          name="title"
          value={title}
          onChange={handleChange}
        />
      </Form.Group>
      {errors?.title?.map((message, idx) => (
        <Alert variant="warning" key={idx}>
          {message}
        </Alert>
      ))}

      <Form.Group>
        <Form.Label>Content</Form.Label>
        <Form.Control
          as="textarea"
          rows={6}
          name="content"
          value={content}
          onChange={handleChange}
        />
      </Form.Group>
      {errors?.content?.map((message, idx) => (
        <Alert variant="warning" key={idx}>
          {message}
        </Alert>
      ))}

      <Button
        className={`${btnStyles.Button} ${btnStyles.Blue}`}
        onClick={() => history.goBack()}
      >
        cancel
      </Button>
      <Button className={`${btnStyles.Button} ${btnStyles.Blue}`} type="submit">
        create
      </Button>
    </div>
  );

  return (
    <Form onSubmit={handleSubmit}>
      <Row>
        <Col className="py-2 p-0 p-md-2" md={7} lg={8}>
          <Container
            className={`${appStyles.Content} ${styles.Container} d-flex flex-column justify-content-center`}
          >
            <h2 className="text-center mb-4">Share your goal in progress</h2>
            <Form.Group className="text-center">
              {image ? (
                <>
                  <figure>
                    <Image className={appStyles.Image} src={image} rounded />
                  </figure>
                  <div>
                    <Form.Label
                      className={`${btnStyles.Button} ${btnStyles.Blue} btn`}
                      htmlFor="image-upload"
                    >
                      Change the image
                    </Form.Label>
                  </div>
                </>
              ) : (
                <Form.Label
                  className="d-flex justify-content-center"
                  htmlFor="image-upload"
                >
                  <Asset className={styles.AssetUpload}
                    src={Upload}
                    message="Click or tap to upload an image"
                  />
                </Form.Label>
              )}

              <Form.File
                id="image-upload"
                accept="image/*"
                onChange={handleChangeImage}
                ref={imageInput}
              />
            </Form.Group>
            {errors?.image?.map((message, idx) => (
              <Alert variant="warning" key={idx}>
                {message}
              </Alert>
            ))}

            <div className="d-md-none">{textFields}</div>
          </Container>
        </Col>
        <Col md={5} lg={4} className="d-none d-md-block p-0 p-md-2">
          <Container className={appStyles.Content}>{textFields}</Container>
        </Col>
      </Row>
    </Form>
  );
}

export default PostCreateForm;

```

the post req is https://odyssey-api-f3455553b29d.herokuapp.com/posts/

with this form-data

```json
{
    "title": "My Test Post (Postman API)",
    "content": "This is a test post content",
    "image": "test_image.jpg"
}
```

which returns

{
    "id": 47,
    "owner": "postmanuser",
    "is_owner": true,
    "profile_id": 24,
    "profile_image": "https://res.cloudinary.com/dh5lpihx1/image/upload/v1/media/images/default_profile_dqcubz.jpg",
    "created_at": "27 Aug 2024",
    "updated_at": "27 Aug 2024",
    "title": "My Test Post (Postman API)",
    "content": "This is a test post content",
    "image": "https://res.cloudinary.com/dh5lpihx1/image/upload/v1/media/images/test_image_aukhfj",
    "image_filter": "normal",
    "like_id": null
}

# 4. new MessageDetailSendForm

Messagedetail form has now been updated to include an image input field.

```jsx
// src/pages/messaging/MessageDetailSendForm.js

import React, { useState, useRef } from "react";
import { useParams } from "react-router-dom";
import { axiosReq } from "../../api/axiosDefaults";
import Button from "react-bootstrap/Button";
import Form from "react-bootstrap/Form";
import Alert from "react-bootstrap/Alert";
import Container from "react-bootstrap/Container";
import Image from "react-bootstrap/Image";
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faPaperPlane, faImage } from '@fortawesome/free-solid-svg-icons';
import axios from 'axios'; 

function MessageDetailSendForm({ setMessages }) {
  const { id } = useParams();
  const [formData, setFormData] = useState({
    content: "",
    image: "",
  });
  const { content, image } = formData;
  const [errors, setErrors] = useState({});
  const imageInput = useRef(null);

  const handleChange = (event) => {
    setFormData({
      ...formData,
      [event.target.name]: event.target.value,
    });
  };

  const handleImageChange = (event) => {
    if (event.target.files.length) {
      URL.revokeObjectURL(image);  // Clean up previous image
      setFormData({
        ...formData,
        image: URL.createObjectURL(event.target.files[0]),  // Create URL for the new image
      });
    }
  };

  const handleSubmit = async (event) => {
    event.preventDefault();
  
    try {
      console.log('Attempting to send message...');
      
      // Create FormData and send it
      const formData = new FormData();
      formData.append("content", formData.content);
      formData.append("image", formData.image);
      
      const response = await axios.post("/api/messages", formData, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      });
      
      console.log('Message sent successfully:', response.data);
  
      // Reset form
      setFormData({ content: "", image: "" });
    } catch (err) {
      console.error("Error sending message:", err);
      if (err.response?.status !== 401) {
        setErrors(err.response?.data);
      }
    }
  };

  return (
    <Container>
      <Form onSubmit={handleSubmit}>
        <Form.Group>
          <Form.Label>New Message</Form.Label>
          <Form.Control
            as="textarea"
            rows={3}
            name="content"
            value={content}
            onChange={handleChange}
            placeholder="Type your message here..."
          />
        </Form.Group>

        {/* Image preview and file input */}
        <Form.Group>
          {image ? (
            <div className="text-center">
              <Image src={image} rounded fluid />
              <Button
                variant="secondary"
                onClick={() => imageInput.current.click()}
              >
                Change Image
              </Button>
            </div>
          ) : (
            <Form.Label htmlFor="image-upload" className="d-flex justify-content-center">
              <FontAwesomeIcon icon={faImage} /> Click to Upload Image
            </Form.Label>
          )}

          <Form.File
            id="image-upload"
            accept="image/*"
            onChange={handleImageChange}
            ref={imageInput}
            className="d-none"
          />
        </Form.Group>

        {errors?.content?.map((message, idx) => (
          <Alert variant="warning" key={idx}>
            {message}
          </Alert>
        ))}
        {errors?.image?.map((message, idx) => (
          <Alert variant="warning" key={idx}>
            {message}
          </Alert>
        ))}

        <div className="d-flex justify-content-between">
          <Button variant="secondary" onClick={() => imageInput.current.click()}>
            <FontAwesomeIcon icon={faImage} /> Add Image
          </Button>
          <Button variant="primary" type="submit">
            <FontAwesomeIcon icon={faPaperPlane} /> Send
          </Button>
        </div>
      </Form>
    </Container>
  );
}

export default MessageDetailSendForm;
```

In summary, what has been changed is the addition of an image input field and the handling of the image in the form data.


# 5. testing passed

I have created a jest file to test the new form with one unit test

```jsx
import React from "react";
import { render, fireEvent, screen, waitFor } from "@testing-library/react";
import axios from "axios";
import MessageDetailSendForm from "../MessageDetailSendForm";
import { MemoryRouter } from "react-router-dom";

// Mock axios
jest.mock("axios");

// Mock URL.createObjectURL and URL.revokeObjectURL
global.URL.createObjectURL = jest.fn(() => "mockedImageURL");
global.URL.revokeObjectURL = jest.fn();

describe("MessageDetailSendForm", () => {
  // Clear mocks before each test
  beforeEach(() => {
    jest.clearAllMocks();
  });

  it("should submit a message with image successfully", async () => {
    // Mock axios.post success response
    axios.post.mockResolvedValueOnce({
      data: { message: 'Success' }
    });

    render(
      <MemoryRouter>
        <MessageDetailSendForm setMessages={jest.fn()} />
      </MemoryRouter>
    );

    // Simulate typing in the message
    fireEvent.change(screen.getByPlaceholderText("Type your message here..."), {
      target: { value: "Test message with image" }
    });

    // Simulate selecting an image file
    const file = new File(["image-content"], "test-image.jpg", { type: "image/jpeg" });
    const fileInput = screen.getByLabelText(/Click to Upload Image/i);
    fireEvent.change(fileInput, { target: { files: [file] } });

    // Simulate clicking the send button
    fireEvent.click(screen.getByText(/Send/i));

    // Wait for axios.post to be called
    await waitFor(() => expect(axios.post).toHaveBeenCalledTimes(1));

    // Check if axios.post was called with the correct parameters
    expect(axios.post).toHaveBeenCalledWith(
      expect.any(String),
      expect.any(FormData),
      expect.objectContaining({
        headers: {
          "Content-Type": "multipart/form-data"
        }
      })
    );
  });
});
```

