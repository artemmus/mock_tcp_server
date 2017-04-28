Module for unit testing of request to server

An example of usage:

```python
    # ...
    
    def test_timeout(self):
        answer = 'HTTP/1.1 200 OK\n\nHello World!'
        with MockTcpServer(response_delay=2, response_data=answer) as srv:
            mock_url = 'http://{}:{}/'.format(srv.host, srv.port)
            request_ts = time.time()
            self.assertRaises(
                TimeoutError,
                make_request,  # some function that makes HTTP request
                url=mock_url,
                timeout=1
            )
            self.assertAlmostEqual(time.time()-request_ts, 1, delta=0.1)
```
